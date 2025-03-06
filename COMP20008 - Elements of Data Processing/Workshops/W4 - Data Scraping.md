
## Objectives:
- Understand how to navigate HTML page structure
- Use `BeautifulSoup` to extract information


## Unicode Encoding
HTML documents typically use UTF-8 to represent the Unicode standard

Unicode allows some characters to be represented in different ways:
![[unicode.png]]
This is an issue for comparison and analysis so typically we *normalise* the strings.

In Python we can normalise Unicode as follows:
```python
import unicodedata

string = "Example string"

normalised = unicodedata.normalise("NFKD", string)
```


## Regex Pattern Searching

In Python:
```python
import re

re.match(pattern, string) # Only matches if the pattern begins at the start
re.search(pattern, string) # Can match anywhere in the string
re.findall(pattern, string) # Returns all found matches
```




