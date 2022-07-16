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

## Hash map

Alternatively, a hash map can be used to reduce the time complexity to O(n), but since we have to use additional memory for the hash map, space complexity become O(n), instead of O(1) in the brute force solution.

First, define an empty hash map.

Then we can start a loop through the array. The *enumerate* method comes in handy comes in handy here because it provides the index for each number in the array as a key/val pair.

In the loop, we can check to see if the difference between the current value and the target number exists in the hash map. If it isn’t we add the number to the hash map and loop again.

```python
hashmap = {}
for i, num in enumerate(nums):
	diff = target - num
	if diff in hashmap:
		return hashmap[diff], i
hashmap[num] = i
```

Again, both space and time complexity here is O(n).
