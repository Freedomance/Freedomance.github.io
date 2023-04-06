---
title: LeetCode Day01 
tags: C++
---
- No.704 二分查找
- No.27  移除元素
<!--more-->
题目：
 - No.704  二分查找
      - No.35 搜索插入位置 
 - No.27   移除元素


所属模块：
 - 数组
 
基础知识：
 

核心算法：
 - 二分查找 

```C++
//左闭右开 [left, right)
int TwodivideSearch(vector<int>& nums, int target){
    int left=0;
    int right=nums.size() - 1;
    
    while(left < right)
    {
        int middle = (left + right)/2;
        //middle = left + ((right - left) >> 1)  与上式等价 >>移位运算速度更快,三种方法中效率最高
        //middle = left + (right - left)/2
        if(target < nums[middle])
            right = middle - 1;
        else if(target > nums[middle])
            left = middle + 1;
        else    //(target == nums[middle])
            return middle;
    }
    return -1;
}
    
//左闭右闭 [left, right]
int TwodivideSearch(vector<int>& nums, int target){
    int left = 0;
    int right = nums.size() - 1;
    
    while(left <= right)
    {
        middle = left + ((right - left) >> 1);
        if(target < nums[middle]])
            right = middle - 1;
        else if (target > nums[middle]])
            left = middle + 1;                                            
        else
            return middle;
    }
    return -1;
}
```
 - 搜索元素插入位置


```C++
//暴力求解
int SearchInsert(vector<int>& nums, int target){
    for(int i = 0; i <nums.size(); i++){
        if(target <= nums[i])
            return i;    
    }
    return nums.size();
}

//左闭右闭 [left, right]
int SearchInsert(vector<int>& nums, int target){
    int left = 0;
    int right = nums.size() - 1;
    
    while(left <= right)
    {
        middle = left + ((right - left) >> 1);
        if(target < nums[middle]])
            right = middle - 1;
        else if (target > nums[middle]])
            left = middle + 1;                                            
        else
            return middle;
    }
    return right + 1;
}
```
 - 移除元素
   - 初始思路
      - 思路1：查找等于val的元素，将其后的每个元素向前顺移一位
      - 思路2：找到第一个等于val的元素nums[i]后，寻找其后第一个不等于val的元素，将其赋值给nums[i],数组长度减；
      - 思路3：如果要去掉最后一个元素，则push;


```C++
//暴力求解
int removeElement(vector<int>& nums, int val) {
    int newlen = nums.size();
    for(int i = 0; i < newlen; i++){
        if(nums[i] == val){
          for(int j = i + 1; j < newlen; j++){
            nums[j-1] = nums[j];
          }
          i--;
          newlen--;
        }                
    }
    return newlen;     
}

//双指针法（快慢指针） 此指针非彼指针
int removeElement(vector<int>& nums, int val) {
    int slowIndex = 0;
    for(int fastIndex = 0; fastIndex < nums.size(); fastIndex++){
        if(val != nums[fastIndex]){
            nums[slowIndex++] = nums[fastIndex];
        }
    }
    return slowIndex;
}

```



