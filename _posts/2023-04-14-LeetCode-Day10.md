---
title: LeetCode Day10 第五章 栈与队列 part-01
tags: C++
---
理论基础
No.232 用栈实现列表
No.225 用队列实现栈

<!--more-->

# 今日任务 --栈与队列 part-01
- 理论基础
- No.232 用栈实现列表
- No.225 用队列实现栈

# 基础知识
```
- 队列 先进先出
- 栈   先进后出
```
### STL(C++标准库)版本
- HP STL: 其它版本的 C++ STL, 一般是以HP STL为蓝本实现出来的，HP STL是C++ STL的第一个实现版本，而且开放源代码。
- P.J.Plauger STL: 由P.J.Plauger参照HP STL实现出来的，被Visual C++编译器所采用，不是开源的。
- SGI STL: 由Silicon Graphics Computer Systems公司参照HP STL实现，被Linux的C++编译器GCC所采用，SGI STL是开源软件，源码可读性高。(后文在此基础上介绍栈和队列)
### 栈
- 栈提供push和pop等接口，所有元素必须符合先进后出规则；故不提供走访功能，也不提供迭代器；不能像set或map提供迭代器来遍历所有元素。
- 栈以底层容器完成所有的工作，对外提供统一的接口；底层容器是可插拔的(即可以控制使用哪种容器来实现栈的功能)。
- STL中栈往往不被归类为容器，而被归类为容器适配器。
- 栈的底层实现可以是vector、deque、list等容器，主要是数组和链表的底层实现。
- 对于常用的SGI STL，如果没有指定底层实现的话，默认是以deque为缺省情况下栈的底层结构。
- deque: 是一个双向队列，只要封住一端，只开通另一端就可以实现栈的逻辑了。
- 也可以指定vector为栈的底层实现，初始化语句如下：
```
std::stcak<int, std::vector<int>> third;
```
### 队列
- 队列中先进先出的数据结构，同样不允许有遍历行为，不提供迭代器，SGI STL中队列也是以deque为缺省情况下的底层结构。
- STL队列也不被归类为容器，而被归类为容器适配器。
- 也可以指定list为底层实现，初始化queue语句如下：
```
std::queue<int, std::list<int>> third;
```

# 算法核心
## No.232 用栈实现列表
```cpp
class MyQueue{
public:
    stack<int> stIn;
    stack<int> stOut;
    MyQueue(){

    }

    void push(int x){
        stIn.push(x);
    }

    int pop(){
        while(!stIn.empty()){
            stOut.push(stIn.top());
            stIn.pop();
        }
        int result = stOut.top();
        stOut.pop();
        return result;
    }

    int peek(){
        int res = this->pop();
        stOut.push(res);
        return res;
    }

    bool empty(){
        return stIn.empty() && stOut.empty();
    }
}
```
## No.225 用队列实现栈
### 双队列
```cpp
class MyStack{
public:
    queue<int> que1;
    queue<int> que2;
    MyStack(){

    }

    void push(int x){
        que1.push(x);
    }

    int pop(){
        int size = que1.size();
        size--;
        while(size--){
            que2.push(que1.top());
            que1.pop();
        }
        int result = que1.front();
        que1.pop();
        que1 = que2;
        while(!que2.empty()){
            que2.pop();
        }
        return result;
    }

    int top(){
        return que1.back();
    }

    bool empty() {
        return que1.empty();
    }
}
```
### 优化方法-单队列
```cpp
class MyStack{
public:
    queue<int> que;
    MyStack(){

    }

    void push(int x){
        que.push(x);
    }

    int pop(){
        int size = que.size();
        size--;
        while(size--){
            que.push(que.front());
            que.pop();
        }
        int result = que.front();
        que.pop();
        return result; 
    }

    int top() {
        return que.back();
    }

    bool empty() {
        return que.empty();
    }
}

```
