---
title: LeetCode Day08 第四章 字符串 part-01
tags: C++
---
No.344 反转字符串
No.541 反转字符串Ⅱ
剑指Offer No.05 替换空格
No.151 翻转字符串里的单词
剑指Offer No.58-Ⅱ 左旋转字符串
<!--more-->

# 今日任务 --字符串 part-01
- No.344 反转字符串
- No.541 反转字符串Ⅱ
- 剑指Offer No.05 替换空格
- No.151 翻转字符串里的单词
- 剑指Offer No.58-Ⅱ 左旋转字符串  


# 基础知识
## string字符串 和 数组的区别 
- 字符串是若干字符组成的有限序列，也可以理解为一个字符数组
- 在c中，把一个字符串存入数组时，结束符'\0'也存入数组，作为字符串结束的标志
- 在c++中，提供一个string类，其包含size接口，可以用来判断string类字符串是否结束，而无需用'\0'来判断是否结束
## 移除元素
- erase函数的时间复杂度为O(n)
# 算法核心
## No.344 反转字符串
```cpp
void reverseString(vector<char>& s){
    for(int i = 0, j = s.size()-1; i < j; i++, j--){   // i < s.size()/2 
        swap(s[i], s[j]);
    }
}
```

```cpp
// swap() 函数的实现方式

//交换数值
int tmp;
tmp = s[i];
s[i] = s[j];
s[j] = tmp;

//位运算 ?
s[i] ^= s[j];
s[j] ^= s[i];
s[i] ^= s[j];
```
## No.541 反转字符串Ⅱ
```cpp
//使用c++库函数(左闭右开)
string reverseStr(string s, int k){
    for(int i = 0; i < s.size(); i += 2 * k){
        reverse(s.begin() + i, s.begin() + i + k);
    }else{
        reverse(s.begin() + i, s.end());
    }
}

//自定义reverse函数(左闭右闭)
reverse(string& s, int start, int end){
    for(int i = 0, j = s.size()-1; i < j; i++, j--){
        swap(s[i], s[j]);
    }
}

string reverseStr(string s, int k){
    for(int i = 0; i < s.size(); i += 2 *k){
        if(i + k <= s.size()){
            reverse(s, i, i + k - 1);
            continue;
        }
        reverse(s, i, s.size() - 1);
    }
}
```
## 剑指Offer No.05 替换空格
```cpp
string replaceSpace(string s){
    int count = 0;
    int sOldSize = s.size();
    for(int i = 0; i < s.size(); i++){
        if(s[i] == ' '){
            count++;
        }
    }

    s.resize(s.size + count * 2);
    int sNewSize = s.size();
    for(int i = sNewSize - 1, j = sOldSize - 1; i < j; i--, j--){
        if(s[j] != ' '){
            s[i] = s[j];
        }else{
            s[i] = '0';
            s[i - 1] = '2';
            s[i - 2] = '%';
            i -= 2;
        }
    }
    return s;
}
```
## No.151 翻转字符串里的单词
```cpp 
//删除字符串中的空格
void removeExtraSpace(string& s){
    for(int i = s.size() - 1; i > 0; i--){
        if(s[i] == s[i-1] && s[i] == ' '){
            s.erase(s.begin() + i);
        }
    }

    //删除字符串后的空格
    if(s.size() > 0 && s[s.size()-1] == ' '){
        s.erase(s.begin() + s.size() - 1);
    }

    //删除字符串前的空格
    if(s.size() > 0 && s[0] == ' '){
        s.erase(s.begin());
    }
}

void removeExtraSpaces(string& s){
    int slow = 0;
    for(int i = 0; i < s.size(); i++){
        if(s[i] != ' '){
            if(slow != 0)   s[slow++] = ' ';
            while(i < s.size() && s[i] != ' '){
                s[slow++] = s[i++];
            }
        }
    }
    s.resize(slow);
}

```
```cpp
void reverse(string& s, int start, int end){
    for(int i = start, j = end; i < j; i++, j--){
        swap(s[i], s[j]);
    }
}

void removeExtraSpace(string& s){
    for(int i = s.size() - 1; i > 0; i--){
        if(s[i] == s[i-1] && s[i] == ' '){
            s.erase(s.begin() + i);
        }
    }

    //删除字符串后的空格
    if(s.size() > 0 && s[s.size()-1] == ' '){
        s.erase(s.begin() + s.size() - 1);
    }

    //删除字符串前的空格
    if(s.size() > 0 && s[0] == ' '){
        s.erase(s.begin());
    }
}

string reverseWords(string s){
    removeExtraSpaces(s);
    reverse(s, 0, s.size()-1);
    int start = 0;
    for(int i = 0; i <= s.size(); i++){
        if(i == s.size() || s[i] == ' '){
            reverse(s, start, i - 1);
            start = i + 1;
        }
    }
    return s;
}
```
## 剑指Offer No.58-Ⅱ 左旋转字符串
### 思路
假设字符串abcdefg, 左旋前两位字符，得到:cdefgab
- 反转前两位字符:
```
bacdefg
```

- 反转2之后的字符：
```
bagfedc
```

- 反转整个字符
```
cdefgab
```

```cpp
string reverseLeftWords(string s, int n){
    reverse(s.begin(), s.begin() + n);
    reverse(s.begin() + n, s.end());
    reverse(s.begin(), s.end());

    return s;
}
```
