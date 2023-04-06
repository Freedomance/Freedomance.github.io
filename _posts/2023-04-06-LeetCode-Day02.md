---
title: LeetCode Day02
tags: C++
---
- No.977 有序数组的平方
- No.209 长度最小的子数组
- No.59  螺旋矩阵II
<!--more-->
### 题目：
 - No.977 有序数组的平方
 - No.209 长度最小的子数组
 - No.59  螺旋矩阵Ⅱ 

### 所属模块：
 - 数组

### 核心算法
  - 有序数组的平方
    - 初始思路
      - 关键点：①求平方 ②排序 

```cpp
// 暴力求解
vector<int> sortedSquares(vector<int>& nums){
    for(int i = 0; i < nums.size(); i++){
        nums[i] *= nums[i];
    }
    sort(nums.begin(), nums.end());
    return nums;
}

//双指针法
vector<int> sortedSquares(vector<int>& nums){
    vector<int> result(nums.size(), 0);
    int k = nums.size() - 1;
    for(int i = 0, j = nums.size() - 1; i <= j;){
        if(nums[i] * nums[i] > nums[j] * nums[j]){
            result[k] = nums[i] * nums[i];  //result[k--] = nums[i] * nums[i];
            i++;
            k--;
        }
        else{
            result[k--] = nums[j] * nums[j];
            j--;
        }
    }
    return result;
}
```



