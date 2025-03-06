
## Text Processing - Continued


### Ngram processing and string matching

**(Word) ngram** - A series of length *n* words
**Letter ngram** - A substring of length *n* letters


Let $G_n$ be a function that returns all letter-ngrams of length $n$
$G_2(crab) = \texttt{\{\#c, cr, ra, ab, b\#\}}$
$G_3(crab) = \texttt{\{\#\#c, \#cr, rab, ab\#, b\#\#\}}$\
Where # is a padding character

#### Similarity comparison with letter ngrams

Letter ngram distance between words $x$ and $y$ is:
$$|G_n(x)| + |G_n(y)| - 2 \times |G_n(x) \cap G_n(y)|$$

$| \ G_2(crab) \ | = 5$
$| \ G_2(crba) \ | = 5$
$| \ G_2(crab) \cap G_2(crba) \ | = 2$

Bi-gram distance between `crab` and `crba`:
$=5+5-2\times(2)$
$=6$

#### Problems with letter ngram distance
Potentially useful for *approximate* prefixes e.g. Street -> St; Smog -> Smoke
Isn't sensitive to relative ordering of strings (formula doesn't care about position)
Isn't useful for very long words


### Other similarity measures
- Jaccard
- Sorensen-Dice
- Cosine

Distance metrics:
- Levenshtein


In all cases, $\text{Similarity} = 1-\text{distance}$


**Jaccard Similarity**:
$$sim_{jac}(S_1, S_2)=\frac{|S_1 \cap S_2|}{|S_1 \cup S_2|}$$

**Sorenson-Dice**:
$$sim_{dice}(S_1, S_2) = \frac{2\times|S_1 \cap S_2|}{|S_1| + |S_2|}$$

**Cosine Similarity**:

First, vectorise the letter ngrams and tabulate

Let X = "crat", Y = "cart"

|     | \#c | ar  | at  | ca  | cr  | ra  | rt  | t\# |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| X   | 1   | 0   | 1   | 0   | 1   | 1   | 0   | 1   |
| Y   | 1   | 1   | 0   | 1   | 0   | 0   | 1   | 1   |

$$sim_{cos}(X,Y)=\frac{X \cdot Y}{||X||\times||Y||}$$

To compute the dot product, count all of the letter ngrams that appear in *both* words
e.g.  $X\cdot Y = 1+0+0+0+0+0+0+1 = 2$

$||X||=\sqrt{\sum^{n}_{i=1}X_i^2} = \sqrt{1^2+0^2+1^2+0^2+1^2+1^2+0^2+1^2}=\sqrt{5}$


#### Minimum edit distance
How many insertions/deletions/replaces need to be made to transform $X \mapsto Y$?

Levenshtein distance is an algorithm to do this with the 3 basic operations:
- Insert
- Delete
- Replace

We can compute similarity from *normalised* edit distance:

$\text{Similarity} = 1 - \text{normalised distance}$
Where
$$dist_{norm} = \frac{d(S_1, S_2)}{max(|S_1|, |S_2|)}$$

**Example**:
Computing the similarity of $\texttt{ther}\mapsto \texttt{otter}$

|     | t   | h   | e   | r   |
| --- | --- | --- | --- | --- |
| o   | t   | t   | e   | r   |
$sim_{edit}(\texttt{ther}, \texttt{otter})=1.0- \frac{2}{5} = 0.6$

### Uses for approximate string matching
1. Spelling correction
2. Neologisms
3. Word equivalence

#### Dealing with Neologisms

Neologisms could be new words entirely (e.g. 'phat', 'chatGPT') or just portmanteaus (e.g. 'brunch', 'spork')

Language changes constantly.

There is no simple solution to this.


## Regex
Used for finding patterns

In Python:
```python
import re
text = "Hi, my name is Julian!, what is yours?"
name = re.findall(r"name is ([a-zA-Z]*)", text)
print(name)
```

Here you need a capture group!

**Special Characters:**
- `\w` any 'word' character
- `\d` any digit
- `\s` any blank space
- `|` for conjunction
- `.` single character wildcard
- `[]` specify a set
- `^` negation (set complement)
- `()` capture group
- `{num}` specifying number of repetitions
- `*` repetition wildcard (any number of)
- `^` anchor to the *start* of the string **OUTSIDE SQUARE BRACKETS**
- `$` anchor to the *end* of the string
- `\1`, `\2`, `\3`, etc allows retrieval of previous matches in Python