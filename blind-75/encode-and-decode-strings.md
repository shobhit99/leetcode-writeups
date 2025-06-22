# Encode and decode strings

### Explanation
- We will calculate the length of each word
- We will add that to the string as "{lenght},{word}"
- We will keep appending to the encoded string for all words
- While decoding
- We will get the number first i.e until , and iterate that number of indexes to form the word
- keep repeating until the end of the string

### Code
```python
class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """
        output = ""
        for word in strs:
            str_len = len(word)
            output += "{},{}".format(str_len,word)
        return output

    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """
        output = []
        i = 0
        while i < len(s):
            number = ""
            word = ""
            while s[i] != ",":
                number += s[i]
                i += 1
            number = int(number)
            for j in range(number):
                i += 1
                word += s[i]
            output.append(word)
            i += 1
        return output
        


# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(strs))
```