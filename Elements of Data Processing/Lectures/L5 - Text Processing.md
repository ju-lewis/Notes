

## The Unstructured Text Pipeline:
1. Crawler collects pages
2. Scraped out desired HTML - leaving you with strings of text
3. Now you want to:
	1. Break up sentences and words
	2. Standardise words in various ways (e.g. no past tense, etc.)
	3. Remove unnecessary material
4. Now you can process your text


## Text Preprocessing Sequence

### Sentence Splitting
Split the string when two words are separated by one of: "`.`", "`?`", "`!`"  and sometimes when the second string starts with a capital letter.

Exceptions:
- "etc." - the full stop doesn't denote the end of a sentence

### Word Splitting (Tokenisation)
The goal is to split a sentence into word tokens

*Delimiter* := " "

One issue is that punctuation makes the same word result in different tokens!
e.g. "hello" and "hello!" are different tokens

So we strip off punctuation as separate token using Regex


**Normalisation (case folding)**
Goal: Convert text to lower case

This reduces sparsity (as more words will map to the same lower-case form)
This is simple and effective for many tasks
Supports search and matching
### Word Regularisation (lemmatising)

**Problem 1**: English has different forms of the same word - tense, plurality, aspect
e.g. Driving vs Drive vs Drives vs Drove

**Problem 2**: Words in English are often compounds of a **stem** and several **morphemes**
e.g. *Inexpensive* is composed of `in`+`expense`+`ive`

Treating each of these separately makes the lexicon much larger!

<hr>

**Solution 1 (Simple)**: use a stemmer to chop of certain parts of words
- "-s", "-es", "-ed", "-ing", "-en"
This is very suboptimal as you'll result in incorrect parsing: e.g. "ring" $\rightarrow$ "r"
Can't modify tense

**Solution 2 (Lemmatiser)**: Converts each word to its root form (lemma)
- Plural $\mapsto$ Singular (e.g. "cars" $\rightarrow$ "car")
- Verbs lose tense (e.g. "ate" $\rightarrow$ "eat")

<hr>

In this subject we'll use the **Porter Stemmer**

For lemmatising, tools are either carefully manually built with many implemented rules, or machine learning-based demorphers

#### Open-class and Closed-class Words
Some words provide *content*, others provide grammatical *function*
- Open-class: provide content (e.g. bike, car, tree)
- Closed-class: provide function (e.g. the, to, not, and, they)

We typically want to remove closed-class words because we only care about content topics

**Stopword lists** contain the closed-class words you want to remove
This allows for more accurate clustering and feature reduction

>[!tldr] Python Libraries
>1. **Python NLTK** - General word processing library
>2. **ranks.nl** - Provides stopword lists
### Ngram processing and string matching

