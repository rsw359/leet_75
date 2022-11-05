# Longest Consecutive Sequence

Leet problem 129

Given an unsorted array of integers, return *the length of the longest consecutive elements sequence.*

You must write an algorithm that runs in `O(n)` time.

Example 1:

```
Input: nums = [100,4,200,1,3,2]
Output: 4

Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. 
Therefore its length is 4.
```

The best place to start is to determine if a given number in the array is the beginning of a sequence. That can be done by checking if the the *consecutive number to the left* exists within the array. 

In the example, the consecutive number to the left on 100, which would be 99, does not exist within the array. The **length** can be initialized to a variable. 

Next the check for the following consecutive number, 101. This does not exist in the array, so the length of the current sequence is 1. We then add one to the length, then move on to the next number in the array. 

The next number in the array’s previous consecutive number *does exist* in the array, so we move on to the next number and begin the checks again. 

The input array can be converted to a set for efficiency.

The longest sequence can be set to a variable, and after all values have been checked, the sequence with the max length can be obtained. 

Solution:

```python
nums = [100, 4, 200, 1, 3, 2 ]

numSet = set(nums) #convert to set
longest = 0 #initialize to zero

for num in nums:
	if (num - 1) not in numSet:
		length = 0 
		while (num + length):
			length += 1
			longest = max(length, longest)
	return longest
```

Time Complexity

Since we can obtain the longest consecutive sequence by only passing through our array once, this algorithm has time complexity of O(n) where n is the length of the input array. The space complexity is O(n) as well, since we did have to create the set in memory.