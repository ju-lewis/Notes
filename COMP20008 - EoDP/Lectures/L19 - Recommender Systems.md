

## Why Recommender Systems?

Scarcity to abundance
Internet changed shopping behaviours

Now, businesses are heavily reliant on recommender systems.



75% of what people watch is some sort of recommendation (Netflix)


## Methods of Recommendation

### Popularity based recommendation
Very simple
Not personalised

Everyone is recommended the same things.

### Collaborative Filtering

Making predictions about a user's missing data according to the collective behaviour of many other users.
- Look at collective behaviour (ratings)
- Active user history
- *Combine!*


Given a set of $m$ users ($U$) and a set of $n$ items ($I$) we can create an $m\times n$ matrix of ratings. (users = rows, items = columns)
	Our goal is to fill in the missing entries.
	
#### Item-Based Collaborative Filtering

How do we measure item similarity?
- Euclidean distance with *mean imputation*
	- The matrix is incredibly sparse, so we need to perform a lot of imputation

$$sim(i_i, i_j) = \frac{1}{1+d(i_i,i_j)}$$
where $d(i_i, i_j)$ is euclidean distance between the 2 items.


**Predicting what a user what rate an unknown item:**
Given target user $a$ has rated some items, choose a number $k$ and select the $k$-most similar items (that the user *has* rated) to the current unknown item we're checking.


##### Phase 1
- For each item $j$, compute similarities between $j$ and other items

This is *extremely* computationally expensive, so it is run off-line and using batch processing.
##### Phase 2
Predict rating of item $j$ by user $a$

This is pretty efficient, and is performed on-line


>[!note]
>How do we handle new (unrated) items? (Cold-start problem)
>
>We can randomly introduce the content to users to get recommendations.



#### User-Based Collaborative Filtering
Very similar to item-based

For each user, compute their similarity to all other users.


>[!tldr] Summary
>Typically item-based collaborative filtering performs better.
>
>- Item ratings are more 'static' than user preferences
>- User-based has scaling issues as user count increases


### Downsides of Content-Based Approach

Content-based recommendation
- Relies on the properties of items
	- Need solid profiles
	- Can be hard to choose
- Transparency issues
- Independent from other user's ratings
	- Can recommend unpopular things to the user if they're similar enough


We can combine these recommendation techniques using the *matrix method*


### Other issues in deployment of recommendations
- How to be fair to rare items
- How to avoid only recommending popular items

How do we quantify how good the recommendations are?
- RMSE with actual rating vs predicted rating
