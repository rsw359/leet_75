# Product of Array Except Self

Leet Problem 238

Given an integer array `nums`, return *an array* `answer`*such that* `answer[i]`*is equal to the product of all the elements of* `nums` *except* `nums[i]`.

The time complexity for the solution must be O(n).

```python
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

A good way to solve this problem is to pass over the list and multiply the product of the  proceeding indexes by the current index, saving the products to a list. Then do the same, but this time iterating over the from the last index, saving the products to a separate list. We could call them prefix and postfix respectively.

## prefix

nums = [1, 2, 3, 4]

Start with a default of 1. 1 multiplied by 1; 2 multiplied by 1; 3 multiplied by 2; 4 multiplied by 6

prefix = 1, 2, 6, 24

## postfix

Start with a default of one, but from the last index. 4 multiplied by 1; 3 multiplied by 4; 2 multiplied by 12; 1 multiplied by 24

postfix = 24, 24, 12, 4

Finally, take the product of the prefix and postfix for each index(ignoring the value for the current index) and store it in the results list that will be returned.

For index 0, which is 1(again using the default invisible 1 as there is no preceding value): 1 multiplied by 24

For index 1: 1 multiplied by 12

For index 2: 2 multiplied by 4

For index 3: 6 multiplied by the default 1(which is invisible as this is the end of the list)

Results = [24, 12, 8, 6]

The time complexity is O(n). The space complexity is the same since we have to use memory to store the two lists. This can be done in O(1) space time if we pass over the input list twice, and update the results list instead of storing the values separately.

## prefix (pass 1)

nums = [1, 2, 3, 4]

Start with a default of 1 at index 0  in *results*.

For index 0 in *nums*: 1(default prefix) multiplied by 1 (current index in nums), then update the **prefix** variable by multiplying it by the index value and storing it in the next index in the *results* list. Index 1 in *results* has a value of 1.

For index 1 in *nums*: 1(current prefix) multiplied by 2(current index in *nums*). The product is stored at index 2 in *results.* Prefix variable is updated to 2 * 1.

For index 2 in *nums*: 3(current index in nums)*2(current prefix) = 6. 6 is stored at index 3 in*results*. Prefix is updated to 6

For index 3 in *nums*: 4*6 = 24.  This product is not stored because we have reached the end of the list. Now for pass two

results = 1, 1, 2, 6

## postfix (pass 2)

nums = [1,2,3,4]

results = [1, 1, 2, 6]

postfix = 1

Start with a default of one, but from the last index. This time, we multiply the numbers in the same index position in *results* by the **postfix**. Then update the postfix by  multiplying it by the index value in nums

For index 3: 6 multiplied by 1(the default **postfix** variable). Then update the prefix by multiplying 4(current index in *nums*) by 1 (the current postfix)

For index 2: 2( current index in *results*) multiplied by 4(current postfix). Postfix is updated to 3(current index in *nums*) by 4 (the current **postfix**)

For index 1: 1( current index in *results*) multiplied by 12(current **postfix**). Postfix is updated to 2(current index in *nums*) by 12 (the current **postfix**)

For index 0: 1( current index in *results*) multiplied by 24(current **postfix**). No more postfix updates are needed

results = 24, 12 ,8, 6

Again, the time complexity is O(n), and space complexity is O(1).

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        result = [1] * len(nums)#initialize the output to the length of the input
        
        prefix = 1 
        for i in range(len(nums)):
            result[i] = prefix #update results
            prefix *= nums[i] # multiply index in nums by the prefix to update pre
        
        postfix = 1
        for i in range(len(nums) -1, -1, -1):
            result[i] *= postfix #mult the prev result by the postfix
            postfix *= nums[i] # multiply index in nums by the post to update post
        return result
```
