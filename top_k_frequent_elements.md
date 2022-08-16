# Top K Frequent Elements

Leet problem 347

Given an integer array `nums`and an integer `k`, return *the*`k` *most frequent elements*.

**Example 1:**

```python
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

In order to solve this problem we can use a dictionary that associates the count of each item in our input list with the value of each item. The key will be the count, for example:

| key | value |
| --- | --- |
| 3 | 1 |
| 2 | 2 |
| 1 | 3 |

```python
count ={}
for n in nums:
count[n] = 1 + count.get(n, 0)
```

Once we have created the hash table, we can then append the keys and values to a list. The length of the list will be bound by the length of the input list. The example list contains 6 items.

```python
frequency = []
for num, counted in count:
	frequency[counted].append(num)

```

Finally, we can return the results. We only want the k number of most frequently occurring values, so we will specify that.

```python
results = []
for i in range(len(frequency)-1,0,-1):
	for n in frequency[i]:
		results.append(n)
		if len(results) == k:
			return results
```

The full solution:

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = {}
        freq = [[] for i in range(len(nums) +1) ]
        
        for n in nums:
            count[n] = 1 + count.get(n, 0)
        for n, c in count.items():
            freq[c].append(n)
            
        res = []
        
        for i in range(len(freq) -1, 0, -1):
            for n in freq[i]:
                res.append(n)
                if len(res) == k:
                    return res
```

## Big O

The time complexity for this solution is linear. Since we create the hash map, and the list of key value pairs, we have a complexity of O(2n), but of course we drop the constant. Both time and space complexity is O(n).