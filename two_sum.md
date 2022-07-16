# Two Sum

Leet problem 1

Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have ***exactly* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

**Example 1:**

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

```

## Brute Force

The brute force way to solve this problem is to use a nested loop, the outer loop checking each index in the array, the inner loop adding the remaining numbers in the array one by one till the sum equals the target number. Because this solution uses a nested loop, the time complexity becomes O(n^2). 

##