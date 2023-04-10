---
title: LeetCode Day04 第二章 链表
tags: C++
---
链表    No.24 两两交换链表中的节点    No.19 删除链表的倒数第N个节点    面试题 02.07. 链表相交    No.142 环形链表Ⅱ    总结
<!--more-->
# 今日任务 --链表
## No.24 两两交换链表中的节点
## No.19 删除链表的倒数第N个节点
## 面试题 02.07. 链表相交
## No.142 环形链表Ⅱ 
## 总结

# 基础知识
# 算法核心
## No.24 两两交换链表中的节点
### 想法
 - 相对容易, 但需注意细节
```cpp
ListNode* swapPairs(ListNode* head){
    ListNode* dummyHead = new ListNode(0);
    dummyHead->next = head;
    ListNode* cur = dummyHead;

    while(cur->next && cur->next->next){  //先判断cur->next, 后判断cur->next->next, 以防访问空指针报错
        ListNode* tmp = cur->next;
        ListNode* tmp1 = cur->next->next;

        cur->next = cur->next->next;
        cur->next->next = tmp;
        cur->next->next->next = tmp1;

        cur = cur->next->next;
    }
    return dummyHead->next;
}
```

## No.19 删除链表的倒数第N个节点 
### 想法
 - 解题思路实在精妙
```cpp
ListNode* removeNthFromEnd(ListNode* head, int n){
    ListNode* dummyHead = new ListNode(0);
    dummyHead->next = head;
    ListNode* slow = dummyHead;
    ListNode* fast = dummyHead;
    n = n + 1;
    while(n-- && fast){
        fast = fast->next;
    }

    while(fast){
        fast = fast->next;
        slow = slow->next;
    }

    ListNode* tmp = slow->next;
    slow->next = tmp->next;
    delete tmp;

    return dummyHead->next;
}

```

## 面试题 02.07. 链表相交
### 初始思路
 - 第一个链表的每一个节点的指针域，分别与第二个链表中的每一个节点的指针域做比较，指针域相同时起指向的节点即为两链表的交点
### 新思路
 - 分别计算两个链表的长度，然后移动遍历长链表的指针，使两链表末尾对齐；
 - 同时移动遍历两链表的指针，并逐个对比其是否相同，当指针相同时，找到交点；
```cpp
ListNode* genIntersectionNode(ListNode* headA, ListNode* headB){
    ListNode* curA = headA;
    ListNode* curB = headB;
    int lenA = 0, lenB = 0;
    while(curA){
        lenA++;
        curA = curA->next;
    } 
    while(curB){
        lenB++;
        curB = curB->next;
    }

    curA = headA;
    curB = headB;
    if(lenB > lenA){
        swap(lenA, lenB);
        swap(curA, curB);
    }

    int gap = lenA - lenB;
    while(gap--){
        curA = curA->next;
    }
    while(curA){
        if(curA == curB){
            return curA;
        }
        curA = curA->next;
        curB = curB->next;
    }

    return NULL;
}

```

## No.142 环形链表Ⅱ
### 思路
 - 此题较难，思路清奇，难以想到
 - 通过双指针判断链表是否有环，如果有环，快慢指针必然会在链表中的某个节点处相遇； 
```cpp
ListNode* detectCycle(ListNode *head){
    ListNode* fast = head;
    ListNode* slow = head;
    while(fast && fast->next){
        slow = slow->next;
        fast = fast->next->next;
        if(slow == fast){
            ListNode* index1 = slow;
            ListNode* index2 = fast;
            while(index1 != index2){
                index1 = index1->next;
                index2 = index2->next;
            }
            return index1;
        }
    }
    return NULL;
}

```


