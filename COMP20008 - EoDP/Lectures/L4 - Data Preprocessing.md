## Normalisation vs Standardisation
Normalisation involves scaling based on the max and min values
Standardisation involves warping the scores to a normal distribution

**IS THE DATA NORMALLY DISTRIBUTED??**
Normalisation produces a value between 0 and 1, standardisation scales the distribution.

## Data Entity Resolution
Data entity resolution is the process of determining if data from separate sources refer to the same entity.

>[!example]
>Is "A. Einstein", "Albert Einstein", and "Einstein" the same person?
>
>Typically specialised language processing tools are needed to answer this.

## Missing Data
### Missing Completely at Random (MCAR)
Data is MCAR when there is absolutely no way to predict which records are missing from the dataset.
### Missing at Random (MAR)
Data is MAR when the missing values are loosely coupled to the records, i.e. you can make a statement about which values are missing that's slightly more accurate than a complete guess.
### Missing Not at Random (MNAR)
Data is MNAR when the missing values on a variable are related to the values of that variable itself, even after controlling other variables.
### Disguised Missing Data
Missing data is disguised when there is an entry for the record, however its value is misleading.

This needs to be handled by assessing what values are *unusual*, using knowledge about the domain of the values.

## Imputation and Sampling

### Simple Imputation for Numerical Data:
**Imputation** is the process of 'guessing' missing values.

Statistical Measurement Imputation: Simple strategies to fill out numerical data records:
- Mean
- Median
- Mode
This introduces bias into the data, and is sometimes undesired.

### Sampling from data
Sampling is the process of selecting a few examples to represent all the data
When to sample? *When the dataset is too large to effectively process*
### Sampling methods
- **Randomly sampling:** Choosing random records from the dataset with/without replacement
- **Stratified sampling:** You split the population into groups depending on the relevant features

Sampling challenges:
- Representative - has the same important properties as the population
- Balanced


## Data Capture

### REST APIs
**REST (Representational State Transfer)** APIs
A set of protocols (rules) that format the exchange of information between server and client.

This follows typical HTTP request rules.
- Header
	- Accept:
	- Content-type:
- Body (Not for GET requests)
	- Key-value pairs
	- Text

An HTTP response takes:
- Header
- Content
- Status
### Crawling and Scraping
Web crawlers are known as *spiders*, *crawlers*, or *bots*

Synonym URLs are disregarded - **prevents infinite looping**
Significant/dynamic pages must be visited more frequently

**Basic challenge**: there is no central index of the URLs you want, beginning from a seed all pages must be found organically

#### The Algorithm
Start by creating a data structure of pages to visit:
- Stack -> Depth first search
- Queue -> Breadth first search
- Priority Queue -> 'best' first search

>[!info] Algorithm
>1. Start with a URL
>2. Extract all URLs from the parsed data from the start page
>3. Add to data structure
>4. Visit next page
>5. Remove visited page
#### robots.txt
A file that notifies crawlers what to visit and what not to visit
- `user-agent` identifies which crawler the rules apply to
- `allow` a URL path that may be crawled
- `disallow` a URL path the may **not** be crawler
- `sitemap` the complete URL of a sitemap (map of the server)



What you **MUST** do:
- Only crawl allowed pages
- Respect `robots.txt`
- Be robust (immune to spider traps and malicious server behaviour)
- Be legal

What you **SHOULD** do:
- Be scalable
- Be efficient

### The Scraping Pipeline
1. Crawl the web for documents
2. Scrape info out of the documents
3. Clean and save the info

We can use the Python library `beautifulsoup`

`beautifulsoup` is an HTML parsing library that makes data extraction easy:

```python
# Finding an element by ID:
soup.find(id="test-id")

# Finding all elements
soup.find_all()
```



>[!tldr] Need to Know
>- When to use a spreadsheet vs relational DB
>- Basic preprocessing techniques (scaling, imputation, sampling)
>- REST APIs
>- Website Crawling
>- Scraping with Beautiful Soup
>- Justifications for above techniques

