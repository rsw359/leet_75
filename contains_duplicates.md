# Contains Duplicate

Leet problem 217

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: true

```

**Example 2:**

```
Input: nums = [1,2,3,4]
Output: false
```

One solution involves using a hash map, taking the count of each character, and checking if any character has a count of 2 or more.

## Using A Hash Map

The Time complexity of this solution is O(n), since we do take a count of each number in the list. Space complexity likewise would be O(n) because we created a hash map and populated it with one key/value pair for each item in the list.

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
 # create an empty hash table, use get to get the keys and add 1 for each time 
 # the number is encountered
        nums_hash = {}
        for i in range(len(nums)):
            nums_hash[nums[i]] = 1 + nums_hash.get(nums[i], 0)
 # check the value for each key, if it's 2 or greater, return true
        for num in nums:
            if nums_hash[num] >= 2:
                return True
        return False
```

The run time for this is 633 ms and used 26MB of memory.

## Using A Set

 A faster and (*slightly*) more efficient way to do this is to use a set and check whether the number in the list exists in the set. If it does, return True immediately. The run time is faster, although the time and space complexity remain O(n), where n is the size of the original data set.

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
 # create set
    nums_set = set()
 #check if num is in the set, and if so, return True. Otherwise, add it to the 
 #set and loop again 
    for num in nums:
     if num in num_set:
       return True
     num_set.add(num)
       return False
```

The run time for this solution was 462 ms and used 26 MB of memory.

## Brute Force

The brute force method would be to use a nested loop. We would have to loop through the list, then loop again and check if the subsequent numbers in the list were identical to the initial number from the first loop.

The time complexity would be O(n^2), but we wouldn't need to allocate any additional memory, resulting in a space complexity of O(1).
