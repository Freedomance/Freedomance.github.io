---
title: LeetCode Day02
tags: C++
---
数组  
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

### 基础知识
INT32_MAX

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

 - 长度最小的子数组
  - 有难度，乍一看题目，暴力方法可能也想不出来
 

```cpp
//暴力求解
int minSubArrayLen(int target, vector<int>& nums){
    int result = INT32_MAX;
    int sum = 0;
    int subLength = 0;

    for(int i = 0; i < num.size(); i++){
        sum = 0;
        for(int j = i; j < nums.size(); j++){
            sum += nums[j];
            if(sum >= target){
                subLength = j - i + 1;
                result = result < subLength ? result : subLength;
                break;
            }
        }
    }
    return result == INT32_MAX ? 0 : result;
}

//滑动窗口（双指针），核心在于滑动窗口初始位置i的设定，j为滑动窗口的终止位置
int minSubArrayLen(int target, vector<int>& nums){
    int result = INT32_MAX;
    int sum = 0;
    int subLength = 0;
    int i = 0;

    for(int j = 0; j < num.size(); j++){
        sum += nums[j];
        while(sum >= target){
            subLength = j - i + 1;
            result = result < subLength ? result : subLength;
            break;
        }
    }
    return result == INT32_MAX ? 0 : result;
}
```

- 螺旋矩阵Ⅱ
 - 初始思路：矩阵维度n*n,关键在于如何按螺旋方式遍历1-n
 - 学习视频讲解收获：循环不变量原则

```c++
vector<vector<int>> generateMatrix(int n){
    vector<vector<int>> res(n, vector<int>(n, 0));
    int startx = 0, starty = 0;
    int loop = n/2;
    int mid = n/2;
    int count = 1;
    int offset = 1;
    int i, j;

    while(loop--){
        i = startx;
        j = starty;

        for(j = starty; j < n - offset; j++){
            res[i][j] = count++;
        }
        for(i = startx; i < n - offset; i++){
            res[i][j] = count++;
        }
        for(; j > starty; j--){
            res[i][j] = count++;
        }
        for(; i > startx; i==){
            res[i][j] = count++;
        }
    }

    if(n % 2){
        res[mid][mid] = count;
    }

    return res;
}
```



