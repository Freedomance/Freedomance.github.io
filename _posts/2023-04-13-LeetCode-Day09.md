---
title: LeetCode Day09 字符串 part-02
tags: C++
---
No.28 实现strStr()
No.459 重复的子字符串
字符串总结
双指针回顾
<!--more-->

# 今日任务 --字符串 part-02
- No.28 实现strStr()
- No.459 重复的子字符串
- 字符串总结
- 双指针回顾


# 基础知识
## KMP算法--解决字符串匹配问题
```
例如 给定文本串“aabaabaaf”和模式串“aabaaf”, 求在文本串中是否出现过文本串
```
前缀表
- 前缀 只包含首字符，不包含尾字符的全部子串
```
a aa aab aaba aabaa
```
- 后缀 只包含尾字符，不包含首字符的全部子串
```
f af aaf baaf abaaf
```
- 最长相等前后缀
```
a aa aab aaba aabaa aabaaf
0  1   0    1     2      0
```
- 前缀表
```
010120
```
- next数组: 用前缀表作为next数组
```cpp
void getNext(int* next, const string& s){
    int j = 0;
    next[0] = 0;
    for(int i = 1; i < s.size(); i++){
        while(j > 0 && s[i] != s[j]){
            j = next[j-1];
        }
        if(s[i] == s[j]){
            j++;
        }
        next[i] = j;
    }
}
```

## 移动匹配
```
假设字符串“abcabc”, 判断是否能由其字串的重复而构成
```
- 字符串s = "abcabc", 若能够由子串重复组成，则原字符串必然能从新字符串“s+s”的中间部分找到
```
abcabc -> bcabcabcab
``` 




# 算法核心
## No.28 实现strStr()
```cpp
void getNext(int* next, const string& s){
    int j = 0;
    next[0] = 0;
    for(int i = 1; i < s.size(); i++){
        while(j > 0 && s[i] != s[j]){
            j = next[j-1];
        }
        if(s[i] == s[j]){
            j++;
        }
        next[i] = j;
    }
}
int strStr(string haystack, string needle){
    if(needle.size() == 0){
        return 0;
    }
    int next[needle.size()];
    getNext(next, needle);
    int j = 0;
    for(int i = 0; i < haystack.size(); i++){
        while(j > 0 && haystack[i] != needle[j]){
            j = next[j-1];
        }
        if(haystack[i] == needle[j]){
            j++;
        }
        if(i == needle.size()){
            return (i - neelde.size() + 1);
        }
    }
    return -1;
}
```

## No.459 重复的子字符串
### 移动匹配法
```cpp
bool repeatedSubstringPattern(string s){
    string t = s + s;
    t.erase(t.begin());
    t.erase(t.end() - 1);
    if(t.find(s) != std::string::npos){ //?
        return true;
    }
    return false;
}
```
### KMP求解的思路
- 重复子串的最小单位 = 字符串里最长相等前后缀所不包含的子串

```cpp
void getNext(int* next, const string& s){
    int j = 0;
    next[0] = 0;
    for(int i = 1; i < s.size(); i++){
        while(j > 0 && s[i] != s[j]){
            j = next[j-1];
        }
        if(s[i] == s[j]){
            j++;
        }
        next[i] = j;
    }
}
bool repeatedSubstringPattern(string s){
    if(s.size() == 0){
        return false;
    }
    int next[s.size()];
    getNext(next, s);
    int len = s.size();
    if(next[len-1] != 0 && len % (len - next[len-1]) == 0){
        return true;
    }
    return false;

}
```
## 字符串总结
## 双指针回顾