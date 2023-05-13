---
title: LeetCode Day11 第五章 栈与队列 part-02
tags: C++
---
No.20 有效的括号
No.1047 删除字符串中的所有相邻重复项
No.150 逆波兰表达式求值
<!--more-->

# 今日任务 --xx
- No.20 有效的括号(使用栈解决的经典问题)
- No.1047 删除字符串中的所有相邻重复项(使用栈解决的经典题目)
- No.150 逆波兰表达式求值

# 基础知识
## 逆波兰表达式
```
后缀表达式，运算符写在后面，相当于二叉树中的后序遍历
如：2,1,+,3,*   即：(2+1)*3
```


# 算法核心
## No.20 有效的括号
```cpp
class Solution{
public:
    bool isValid(string s){
        if(s.size() % 2 != 0)   return false;
        stack<char> st;
        for(int i = 0; i < s.size(); i++){
            if(s[i] == '(') st.push(')');
            else if(s[i] == '[') st.push(']');
            else if(s[i] == '{') st.push('}');
            else if(st.empty() || s[i] != st.top()) return false;
            else st.pop();
        }
        return st.empty();
    }
}
```
## No.1047 删除字符串中的所有相邻重复项
```cpp
class Solution{
public:
    string removeDuplicates(string S){
        stack<char> st;
        for(char s:S){
            if(st.empty() || s != st.top()){
                st.push(s);
            }else{
                st.pop();
            }
        }
        string result = "";
        while(!st.empty()){
            result += st.top();
            st.pop();
        }

        reverse(result.begin(), result.end());
        return reverse;
    }
}
```

## No.150 逆波兰表达式求值
```cpp
class Solution{
public:
    int evalRPN(vector<string> & tokens){
        stack<long long> st;
        for(int i = 0; i < tokens.size()>; i++){
            if(tokens[i] == "+" || tokens[i] == "-" || tokens[i] == "*" || tokens[/]){
                long long num1 = st.top();
                st.pop();
                long long num2 = st.top();
                st.pop();
                if(tokens[i] == "+")    st.push(num2 + num1);
                if(tokens[i] == "-")    st.push(num2 - num1);
                if(tokens[i] == "*")    st.push(num2 * num1);
                if(tokens[i] == "/")    st.push(num2 / num1);
            }else{
                st.push(stoll(tokens[i]));
            }
        }

        int result = st.top();
        st.pop();
        return result;
    }
}


```