## Description

International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows: ``"a"`` maps to ``".-"``, ``"b"`` maps to ``"-..."``, ``"c"`` maps to ``"-.-."``, and so on.

For convenience, the full table for the 26 letters of the English alphabet is given below:

```
[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
```

Now, given a list of words, each word can be written as a concatenation of the Morse code of each letter. For example, "cba" can be written as "-.-..--...", (which is the concatenation "-.-." + "-..." + ".-"). We'll call such a concatenation, the transformation of a word.

Return the number of different transformations among all words we have.

**Example:**

**Input:** words = ["gin", "zen", "gig", "msg"]

**Output:** 2

**Explanation:**

The transformation of each word is:
"gin" -> "--...-."
"zen" -> "--...-."
"gig" -> "--...--."
"msg" -> "--...--."

There are 2 different transformations, "--...-." and "--...--.".

**Note:**

- The length of ``words`` will be at most 100.

- Each ``words[i]`` will have length in range ``[1, 12]``.

- ``words[i]`` will only consist of lowercase letters.

## Solutions
```python
class Solution(object):
    def uniqueMorseRepresentations(self, words):
        """
        :type words: List[str]
        :rtype: int
        """
        MORSE = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
        base = ord('a')
        trans = set()
        for w in words:
            t = ''
            for i in w:
                t += morse[ord(i)-base]
            trans.add(t)
        return len(trans)
```

这道题思路很简单。看了答案之后才发现有更简洁的写法。

```python
class Solution(object):
    def uniqueMorseRepresentations(self, words):
        MORSE = [".-","-...","-.-.","-..",".","..-.","--.",
                 "....","..",".---","-.-",".-..","--","-.",
                 "---",".--.","--.-",".-.","...","-","..-",
                 "...-",".--","-..-","-.--","--.."]

        seen = {"".join(MORSE[ord(c) - ord('a')] for c in word)
                for word in words}

        return len(seen)
```
两个意思是一样的，但是官方给出的解法就看起来简洁一下，学习了。