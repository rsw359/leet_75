# Valid Anagram

## Leet problem 242

Given two strings `s` and `t`, return `true` *if* `t` *is an anagram of* `s`*, and* `false` *otherwise*.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once. This is NOT a palindrome.

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

The first thing we want to establish, when determining whether two strings are anagrams of each other, is whether the two are of the same length. 

**Check Length:**

```python
if len(s) != len(t): 
	return False
```

If they aren’t the same length, they cannot be anagrams of each other. 

From there, we know that an anagram will contain the same number of occurrences of each character. The best way to do this is to use a hash table, which will contain key/value pairs for the number of occurrences of each letter.

**Create the Hash Tables:**

```python
char_in_s, char_in_t = {}, {}
```

From there, we need to loop through the strings and get the count for each. We will add 1 to the count each time we encounter the same letter.

**Loop and Keep Count:**

```python
#Since the hash table is empty at first, we need to use Pythons get method 
#to get the keys(letters) since they dont exist in the hash tables yet.
#initially, we only need to check the first string

for i in range(len(s)):
	char_in_s[s[i]] = 1 + char_in_s.get(s[i], 0)
	char_in_t[t[i]] = 1 + char_in_t.get(t[i], 0)
```

Then we just need to compare the two hash tables to make sure that they have the same key/value pairs. We can again use the first string to compare.

**Comparison:**

```python
#since we just used the first string, the second hash table hasn't been 
# we have to use the get method to avoid a key error.
# we iterate through the hash tables and compare the pairs, and if any dont match, 
# we return False
 for char in char_in_s:
		if char_in_s[char] != char_in_t.get(char, 0): 
			return False
 return True 
```

If all the pairs match, we have an anagram and the algorithm returns True.

### Putting it all together

C**ompleted Algorithm:**

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        char_in_s, char_in_t = {}, {}
        
        for i in range(len(s)):
            char_in_s[s[i]] = 1 + char_in_s.get(s[i], 0)
            char_in_t[t[i]] = 1 + char_in_t.get(t[i], 0)
        
        for char in char_in_s:
            if char_in_s[char] != char_in_t.get(char, 0):
                return False
        return True
```

Alternatively, in Python we could use the built-in Sorted or Counter methods as follows:

**Counter:**

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
				return Counter(s) == Counter(t)
```

**Sorted:**

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
				return Sorted(s) == Sorted(t)
```

Counter is slightly more efficient than Sorted, since sorted has to arrange the characters in ascending order.

### Space and Time Complexity

The time complexity will be O(n) since we doing each operation for each character in each string.

It is more accurate to say O(s+t).

Similarly, the algorithm uses additional memory, but it does not grow exponentially.  It is one key/value pair for each character being added to the 2  hash tables. Therefore O(s+t)

Using the ***Counter*** method would be the same since this method creates a hash table in the background.

***Sorting*** methods have a time complexity of O(NlogN).