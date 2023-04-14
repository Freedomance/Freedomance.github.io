---
title: LeetCode Day07 第三章 哈希表
tags: C++
---
No.454 四数相加Ⅱ        No.383 赎金信        No.15 三数之和      No.18 四数之和     总结
<!--more-->

# 今日任务 --哈希表
- No.454 四数相加Ⅱ
- No.383 赎金信
- No.15 三数之和 
- No.18 四数之和
- 总结


# 基础知识
- 元素数值可控，元素个数一定，考虑采用数组

# 算法核心
## No.454 四数相加Ⅱ
```cpp
int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4){
    unordered_map<int, int> umap;
    for(int a : nums1){
        for(int b : nums2){
            umap[a + b]++; //c++特性：如map中不存在元素(a + b), 则先insert(a + b)
        }
    }
    int count;    //for(a, b) 和 for(c, b),使算法实现时间复杂度的最优化
    for(int c : nums3){
        for(int d : nums4){
            if(umap.find(0 - (c + d)) != umap.end()){
                umap[0 - (c + d)]++:
            }
        }
    }
    return count;
}

```
## No.383 赎金信
```cpp
//数组求解
bool canConstruct(string ransomNote, string magazine){
    for(int i = 0; i < magazine.size(); i++){
        for(int j = 0; j < ransomNote.size(); j++){
            if(ransomNote[j] == magazine[i]){
                ransomNote.erase(ransomNote.begin() + j);
                break;
            }
        }
    }
    if(ransomNote.length() == 0){
        return true;
    }
    return false;
}

//哈希
bool canConstruct(string ransomNote, string magazine){
    int record[26];
    for(magazine.length() < ransomNote.length()){
        return false;
    } 
    for(int i = 0; i < magazine.length()>; i++){
        record[magazine[i] - 'a']++;
    }
    for(int j = 0; j < ransomNote.length(); j++){
        record[ransomNote[j] - 'a']--;
        if(record[ransomNote - 'a'] < 0){
            return fasle;
        }
    }
    return true;
}
```
## No.15 三数之和 
```cpp
//哈希法 去重操作复杂，且容易超时，
//双指针法
vector<vector<int>> threeSum(vector<int>& nums){
    vector<vector<int>> result;
    sort(nums.begin(), nums.end());
    for(int i = 0; i < nums.size(); i++){
        if(nums[i] > 0){
            return result;
        }
        if(i > 0 && nums[i] == nums[i-1]){
            continue;
        }
        int left = i + 1;
        int right = nums.size() - 1;
        while(right > left){
            if(nums[i] + nums[left] + nums[right] > 0){
                right--;
            }
            else if(nums[i] + nums[left] + nums[right] < 0){
                left++;
            }
            else{
                result.push_back(vector<int> {nums[i], nums[left], nums[right]});
                while(right > left && nums[right] == nums[right-1]) right--;
                while(right > left && nums[left] == nums[left+1]) left++;

                right--;
                left++;
            }
        }
        
    }
    return result;
}

```
## No.18 四数之和
```C++
vector<vecrot<int>> fourSum(vector<int>& nums, int target){
    vector<vector<int>> result;
    sort(nums.begin(), nums.end());
    for(int k = 0; k < nums.size(); k++){
        if(nums[k] > target && target >= 0){
            break;
        }
        if(k > 0 && nums[k] == nums[k-1]){
            continue;
        }

        for(int i = k + 1; i < nums.size(); i++){
            if(nums[k] + nums[i] > target && target >= 0){
                break;
            }
            if(i > k + 1 && nums[i] == nums[i-1]){
                continue;
            }

            int left = i + 1;
            int right = nums.size() - 1;
            while(right > left){
                if ((long) nums[k] + nums[i] + nums[left] + nums[right] > target){
                    right--;
                }else if((long) nums[k] + nums[i] + nums[left + nums[right]] < target){
                    left++;
                }else{
                    result.push_back(vector<int> {nums[k], nums[i], nums[left], nums[right]});
                }

                while(right > left && nums[right] == nums[right - 1])   right--;
                while(right > left && nums[left] == nums[left + 1]) left++;

                right--;
                left++;
            }
        }
    }
    return result;
}
```