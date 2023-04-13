---
title: LeetCode Day06 第三章 哈希表
tags: C++
---
哈希表理论基础      No.242 有效的字母异位词     No.349 两个数组的交集       No.202 快乐数       No.1 两数之和
<!--more-->

# 今日任务 --哈希表
- 哈希表理论基础
- No.242 有效的字母异位词
- No.349 两个数组的交集
- No.202 快乐数
- No.1 两数之和


# 基础知识
## 哈希表理论基础
### 哈希表(Hash table)
 - 哈希表是根据关键码的值而进行访问的数据结构 
 - 通常用来快速判断一个元素是否出现在集合中
 - 哈希表的关键码对应数组中的索引, 两种数据结构分别通过关键码、索引来实现内部元素的访问和操作
### 哈希函数(Hash function)
 - hashcode可以通过特定的编码方式，将其他数据格式转化为不同的数值, 从而将学生姓名映射为哈希表的索引数字
### 哈希碰撞
 - 哈希碰撞的解决方法
   - 拉链法
   - 线性探测法  
### 常见的三种哈希结构
 - 数组
 - set (集合)
 - map (映射)

```
红黑树是一种平衡二叉搜索树，所以key值是有序的，且不可修改，修改key值会导致整棵树的错乱，故只能删除和增加
```

```
 - 需要使用集合解决哈希问题时，优先使用unordered_set, 其查询和增删效率最优
 - 需要集合时有序的, 选用set
 - 当要求集合不仅有序还有重复数据的话，选用multiset
```
| 集合 | 底层实现 | 是否有序 | 数值是否可以重复 | 能否更改数值 | 查询效率 | 增删效率 |
| --- | --- | --- | --- | --- | --- | --- |
|std::set          |红黑树|有序|否|否|O(log n)|O(log n)|
|std::multiset     |红黑树|有序|是|否|O(log n)|O(log n)|
|std::unordered_set|哈希表|无序|否|否|O(1)     |O(1)|


```
map是key-value的数据结构，在map中，对key有限制，对value没有限制，因为key的存储方式使用红黑树实现
```
|映射|底层实现|是否有序|数值是否可以重复|能否更改数值|查询效率|增删效率|
|---|---|---|---|---|---|---|
|std::map          |红黑树|key有序|key不可重复|key不可修改|O(log n)|O(log n)|
|std::multimap     |红黑树|key有序|key可重复  |key不可修改|O(log n)|O(log n)|
|std::unordered_map|哈希表|key无序|key不可重复|key不可修改|O(1)|O(1)|
```
unordered_set、unordered_map C++11中引入标准库
```
# 算法核心
## No.242 有效的字母异位词
```c++
bool isAnagram(string s, string t){
  int record[26] = {0};
  for(int i = 0; i < s.size(); i++){
    record[s[i] - 'a']++;
  }
  for(int i = 0; i < t.size(); i++){
    record[t[i] - 'a']--;
  }
  for(int i = 0; i < 26; i++){
    if(record[i] != 0){
      return false;
    }
  }
  return true;
}
```
## No.349 两个数组的交集
```c++
//set实现
vector<int> intersection(vector<int>& nums1, vector<int>& nums2){
  unordered_set<int> result_set;  //元素不重复, 可直接实现去除重复元素的操作
  unoedered_set<int> nums_set(nums1.begin(), nums2.end());
  for(num : nums2){
    if(nums_set.find(num) != nums_set.end()){
      result_set.insert(num);
    }
  }
  return vector<int> (result.begin(), result.end());
}

//数组实现
vector<int> intersection(vector<int>& nums1, vector<int>& nums2){
  unordered_set result_set;
  int hash[1005] = {0};
  for(int num : nums1){
    hash[num] =1;  //以数组下标为索引,实现哈希映射
  }
  for(int num : nums2){
    if(hash[num] == 1){
      result_set.insert(num);
    }
  }
  return vector<int> (result_set.begin(), result_set.end());
}

```
## No.202 快乐数
```cpp
int getSum(n){
  int sum = 0;
  while(n){
    sum += (n % 10) * (n % 10);
    n /= 10;
  }
  return sum;
}
bool isHappy(int n){
  unordered_set<int> set;
  while(1){
    int sum = getSum(n);
    if(sum == 1){
      return true;
    }
    if(set.find(sum) != set.end()){
      return false;
    }else{
      set.insert(sum);
    }
    n = sum;
  }
}
```
## No.1 两数之和
```
每当遇到需要判断元素是否出现过，或判断元素是否在集合里出现过的时候，首先考虑用哈希法
```
```c++
vector<int> twoSum(vector<int>& nums, int terget){
  unordered_map<int, int> map;
  for(int i = 0 ; i < nums.size(); i++){
    auto iter = map.find(target - nums[i]);
    if(iter != map.end()){
      return {iter->second, i};
    }
    map.insert(pair<int, int>(nums[i], i));
  }
  return {};
}
```

