
## Combining Data from Different Sources

We can't simply to a database-style join on IDs
- May refer to different things

We need to consider the actual content of the data itself
- However, we can't just look for exact matches - since there could be inconsistencies


**Applications**
- Bibliographic databases
- Security


**Terminology**
- Statistics: record linkage
- Databases: entity resolution


### The Challenge
It's incredibly hard to come up with a unique identifier
It can also be very expensive to compare huge numbers of records ($O(n^2)$)
- Consider trying to find which records match between two 1-billion row databases

**The process:**
1. Preprocess records (e.g. case folding, punctuation removal, etc.)

2. Blocking (reducing number of required comparisons)
>[!example] 
>Take each word from a movie title to create 'blocks', only compare films within the same blocks

Block methods should be: efficient and capture good heuristics for matching

3. Score, compare 2 sets of blocks - measure individual similarities
	- *String*: Could use n-gram similarity, Jaccard, Sorensen-Dice, cosine, etc.
	- *Numeric*: Absolute distance

4. Match: Use a function to turn all similarity metrics into a single score
	- $f: \mathbb{R}^d \mapsto [0,1]$


5. Merge: Combine records


