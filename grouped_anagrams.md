# Group Anagrams

Leet problem 49

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

**Example 1:**

```python
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

One way to solve this problem would be to use sort. By sorting, we could sort “tea” and “eat” and then take the append the words to a list. But, using sort has a time complexity on O(n log n), which isn’t the best.

Using a hash map (dictionary in Python) is more efficient. We can take the count of the occurrences of each character and append the strings that have the same counts to a list.

```python
class Solution:
def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
  result = defaultdict(list)
   for string in strs:
     count = [0] * 26 # a-z
    
     for char in string:
       count[ord(char) - ord("a")] += 1 # ord uses the ASCII value for 
                       # each letter
     result[tuple(count)].append(string)
   
   return result.values()

```

In Python the ***ord method*** gets the ASCII value for the characters. By subtracting the ASCII for the letter a from the value for the character we are looking at, we assign the keys to a value of 1-26.  The value in the dictionary (hash map) is the count of each letter.

Next, the strings with the same counts for each character are grouped together and appended to the result dictionary.

Then, the values from the result dictionary are returned.

The time complexity for this solution is O(l*n) where l is the number of strings in the dataset, and n is the number of characters in the string.

* a sort solution will be added later
