
## Regex - Continued

**Anchors:**
When `^` is not contained in square brackets, it anchors to the start of a string
- Within square brackets (e.g. `[^]`) `^` denotes a set complement

`$` anchors to the end of the string

**Repetition:**
- `{m,n}` at least `m` and at most `n` repetitions
- `*` zero or more
- `+` one or more
- `?` zero or one

**Sub-expressions:**
`()` represents a grouped pattern (capture group)

>[!example]
>*"(.+) Or Not \\1"*
>Executed on
>*"To Be Or Not To Be"*
>
>Will report: ["To Be"]

**Lookahead assertions:**
Allows you to specify what comes immediately after a match
- `(?= )` is a *positive* lookahead assertion. The enclosed expression must also be matched if the preceding pattern matched
- `(?! )` is a *negative* lookahead assertion. The enclosed expression must **NOT** be matched.

>[!example]
>`\d+(?=AUD)` will only match if there is a number followed by `AUD`


## Processing Unstructured Data

Is text *really* unstructured?

How can we see there is a structure?
- Can you scramble the words and have it still make sense?

Text does have a structure! But we need more (preprocessing isn't sufficient).

### Documents as bags of words
We represent documents as *feature vectors* of dimension `n` where `n` is the number of unique words in the document and each value is that word's count
- This is sometimes done *with* the stopwords still present

To get an accurate count we need to perform *preprocessing*:
- Word tokenisation
- Case folding
- Stemming/lemmatising
- Stopword removal
- Punctuation removal

#### Benefits of Bag of Words:
- Simple representation (just integers)
- We just need a long vector 
- Easy to produce
- Easily compare documents
- Works for any language, emoticons, etc.
#### What does Bag of Words miss?
- Sequences (temporal context is lost):
	- "Dog bites man" vs "Man bites dog"
- Semantic context:
	- "Polish" for shoes vs "Polish" the nationality

#### Two ways to represent BoW docs in your program
1. A fixed vector of about 100,000 positions
	1. Everything is clearly defined
	2. Unable to handle new / unknown words
2. A list of pairs
	1. May need more storage than just the counts but will be shorter
	2. Able to handle new / unknown words


Is term frequency good enough? **No**
- Raw frequency varies with document length
- Counts don't capture important (rare) words that would be telling of an unusual document type


#### Vector Similarity (For BoW Document Comparison)
Dimensions with similar values across *all* documents are not considered useful

When there are subsets of documents with similar dimension values, then significant information has been found



#### How can you quantify how *unique* or helpful a word is?
**Clustering** does this for you.

We want to 'reward' word rareness.



$$\text{reward}_{w} = \frac{\text{total number of clusters}}{\text{number of clusters with term}}$$
The smaller the number of clusters with the term, the higher the reward!
This is called document frequency

***HOWEVER***
We are interested in *inverse document frequency*

A word is more helpful if it is more frequent (**TF** goes up with term frequency)
A word is more helpful if it is more localised (**DF** goes down with clusters, so its inverse **IDF** goes up with cluster frequency)

So you simply multiply them:
$$\text{word weight} = \text{tf}\times log(\text{idf})$$

Note that we use $log$ *IDF* to prevent it from having a disproportionate effect.


**Normalising (rescaling) TF.IDF** allows us to compare documents of different lengths.

Remember:
- TF -> How many times does the word appear?
- IDF -> How localised is it?

**Computing:**
Step 1 (Determine rarity)
$$v_t = \text{count}(t)\cdot log(\frac{\text{number of clusters}}{\text{number of clusters with }t})$$
$$\text{totalweight} = \sqrt{\sum_{t}{v_t^2}}$$
$$tf\cdot idf_t = \frac{v_t}{\text{totalweight}}$$

#### TF.IDF Summary
The goal of TF.IDF is to replace raw frequency counts

## Document Processing

If we are able to compute similarity of *any* 2 documents
We can:
1. Sort them into clusters
2. Use one document to find similar ones
3. Put all documents into a collection and arrange them by similarity
4. Use keywords to search for them

