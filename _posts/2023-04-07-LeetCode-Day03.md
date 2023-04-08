---
title: LeetCode Day03
tags: C++
---
链表  
链表理论基础  
No.203 移除链表元素  
No.707 设计链表  
No.206 反转链表  
<!--more-->
# 题目
## No.203 移除链表元素
## No.707 设计链表
## No.206 反转链表

# 所属模块
链表
# 基础知识
## 链表 
 - 是一种通过指针串联在一起的线性结构;
 - 每个节点由两个元素组成：数据域(data)与指针域(存放指向下一个节点的指针);
 - 最后一个节点的指针域指向null(空指针);
 - 链表入口节点成为链表的头节点(head);
## 链表类型
### 单链表
### 双链表
 - 每一个节点有两个指针域，一个指向上一个节点(prev)，一个指向下一个节点(next);
 - 双向查询：既可以向前查询也可以向后查询;
### 循环链表
 - 单链表的基础上，链表首尾相连，即：最后一个节点的指针域指向初始节点;
## 链表的存储方式
 - 与指针不同，链表在内存中不一定是连续分布的；
 - 链表通过指针域的指针来链接内存中的各个节点；
 - 链表中的节点分散于内存中的特定单元中，分配机制取决于操作系统的内存管理
## 链表的定义
```cpp
//单链表
struct ListNode{
    int val; //节点中存储的元素(data)
    ListNode *next; //指向下一个节点的指针(指针域)
    // ListNode(int x) : val(x), next(NULL) {} //节点的构造函数
}
```
 - C++会默认生成构造函数，但不会初始化任何成员变量

```cpp
//通过自定义的构造函数初始化节点
ListNode* head = new ListNode(5);

//默认构造函数初始化节点
ListNode* head = new ListNode();
head->val = 5; 
```
## 链表的操作
### 删除节点
非头节点：假设链表的连续节点为A.B.C,删除节点B
- ① 使A节点的指针域指向C节点
- ② 手动释放B节点，释放这块内存

头节点：假设链表的连续节点为A.B.C,删除节点A
- ① 使头节点的指针域指向B节点(head = head->next)
- ② 手动释放A节点，释放这块内存

虚拟头节点(dummy head)：统一删除节点的方式
 - 创建虚拟头节点，使其指向原始头节点

### 插入节点
## 链表于数组性能对比分析
|   | 插入/删除(时间复杂度) | 查询(时间复杂度) |使用场景|
|:---:|:---:|:---:|:---:|
| 数组 | O(n) | O(1) | 数据量固定，频繁查询，较少增删   |
| 链表 | O(1) | O(n) | 数据量不固定，频繁增删，较少查询 |



# 算法核心
## No.203 移除链表元素 

```cpp
//常规方法
ListNode* removeElements(ListNode* head, int val){
    //删除头节点
    while(head !=NULL && head->val == val){ 
        ListNode* tmp = head;
        head = head->next;
        delete tmp;
    }

    //删除非头节点
    ListNode* cur = head;
    while(cur != NULL && cur->next != NULL){
        if(cur->next->val == val){
            ListNode* tmp =cur->next;
            cur->next = cur->next->next;
            delete tmp;
        }
        else{
            cur = cur->next;
        }
    }
    return head;
}

//创建虚拟头节点
ListNode* removeElements(ListNode* head, int val){
    ListNode* dummyhead = new ListNode(0);
    dummyhead->next = head;
    ListNode* cur = dummyhead;

    while(cur->next != NULL){
        if(cur->next->val == val){
            ListNode* tmp = cur->next; 
            cur->next = cur->next->next;
            delete tmp;
        }
    }
    head = dummyhead->next;
    delete dummyhead;
    return head;
}
```

## No.707 设计链表
```cpp
class MyLinkedList {
public:
    struct LinkedNode {
        int val;
        LinkedNode* next;
        LinkedNode(int val) : val(val), next(nullptr){}
    };

    MyLinkedList() {
        dummyHead = new LinkedNode(0);
        size = 0;
    }
    
    int get(int index) {
        if(index > size-1 || index < 0){
            return -1;
        }
        LinkedNode* cur = dummyHead->next;
        while(index--){
            cur = cur->next;
        }
        return cur->val;
    }
    
    void addAtHead(int val) {
        LinkedNode* newNode = new LinkedNode(val);
        newNode->next = dummyHead->next;
        dummyHead->next = newNode;
        size++; 
    }
    
    void addAtTail(int val) {
        LinkedNode* newNode = new LinkedNode(val);
        LinkedNode* cur = dummyHead;
        while(cur->next != nullptr){
            cur = cur->next;
        }
        cur->next = newNode;
        size++;
    }
    
    void addAtIndex(int index, int val) {
        if(index < 0) index = 0;
        if(index > size) return;
        LinkedNode* newNode = new LinkedNode(val);
        LinkedNode* cur = dummyHead;
        while(index--){
            cur = cur->next;
        }
        newNode->next = cur->next;
        cur->next = newNode;
        size++;
    }
    
    void deleteAtIndex(int index) {
         if (index >= size || index < 0) {
            return;
        }
        LinkedNode* cur = dummyHead;
        while(index--) {
            cur = cur ->next;
        }
        LinkedNode* tmp = cur->next;
        cur->next = cur->next->next;
        delete tmp;
        size--;
    }

private:
    int size;
    LinkedNode* dummyHead;
};
```
## No.206 反转链表  
```cpp
//双指针法
ListNode* reverseList(ListNode* head){
    ListNode* tmp;
    ListNode* pre = NULL;
    ListNode* cur = head;
    while(cur){
        tmp = cur->next;
        cur->next = pre;
        pre = cur;
        cur = tmp;
    }
    return pre;
}

//递归法
ListNode* reverse(ListNode* cur, ListNode* pre){
    if(cur == NULL) return pre;
    tmp = cur->next;
    cur->next = pre;
    return reverse(tmp, cur);
}
ListNode* reverseList(ListNode* head){
    return reverse(head, NULL);
}
```

# 今日总结
 - 程序设计题关键在于破解问题的思路，思路清晰完善，题目自然得解
 - 然后高效简洁的解题思路，并不容易想到
 - 当下宜多加训练，以累积经验
