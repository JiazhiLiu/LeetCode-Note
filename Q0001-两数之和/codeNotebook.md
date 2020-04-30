# 两数之和 

## 描述

给定一个整数数组 `nums` 和一个目标值 `target`，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

## 解答

共有三种解法

### 1. 暴力求解


```python
def twoSum(nums, target):
    for s in range(len(nums)):
        for k in range(s+1, len(nums)):
            if nums[s] + nums[k] == target:
                return [s,k]
```

### 2. 先排序后首尾递进查找
对于单调递增数列$a_i (i=0,1,\cdots,n)$，且存在$0\leq i<j\leq n$使得$a_i+a_j=t$，令$s=\min\{i~|~a_i+a_j=t, 0\leq i<j\leq n\}$，$k=\max\{j~|~a_i+a_j=t, 0\leq i<j\leq n\}$，显然$a_s+a_k=t$。对于$i\leq s$，$a_i+a_j$随$j$的减小而减小，其值与$t$的关系未知，但必有$a_i+a_k\leq t$。



```python
def twoSum(nums, target):
    le, s1, s2 = len(nums), 0, len(nums)-1
    nums = sorted(list(enumerate(nums)), key=lambda x: x[1])
    while s1 < s2 and nums[s1][1] + nums[s2][1] != target:
        while s1 < s2 and nums[s1][1] + nums[s2][1] > target:
            s2 = s2 - 1
        while s1 < s2 and nums[s1][1] + nums[s2][1] < target:
            s1 = s1 + 1
    return [nums[s1][0], nums[s2][0]]
```

### 3. 哈希表

* 利用set


```python
def twoSum(nums, target):
    nums_set = set(nums)
    for i, x in enumerate(nums):
        if target - x in nums_set: 
            try:
                return [i, nums.index(target -x, i+1)]
            except ValueError:
                continue
```

* 利用dict


```python
def twoSum(nums, target):
    hash_map = {}
    for i, x in enumerate(nums):
        if target - x in hash_map:
            return [i, hash_map[target-x]]
        else:
            hash_map[x] = i
```
