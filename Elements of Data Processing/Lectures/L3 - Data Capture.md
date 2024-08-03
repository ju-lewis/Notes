
## Numerical Data:
- Countable => discrete (year, )
- Not easily countable => continuous (share price, people in city, temperature, etc.)
## Non-Numerical Data:
- Nominal data => categorical data with no intrinsic ordering

>[!example] Exercise
>Convert an XML snippet to a JSON object.
>
>**Solution:**
>```json
>{
>	"Person": 
>	{
>		"FirstName": "Homer",
>		"LastName": "Simpson",
>		"Relatives": [
>			"Grandpa", "Marge", "Lisa", "Bart"
>		],
>		"FavouriteBeer": "Duff"
>	}
>}
>```


## Ingesting Structured Data
1. Determine the layout of your input data *(DB schema)*
2. Determine semantic types *(e.g. does a number refer to an age, date, temp, etc.)*
3. Define internal data structures *(how will you store the data?)*
4. Write code to ingest the input data into the structure, line by line *(Jupyter notebook)*
5. Preprocessing:
	1. Data cleaning
	2. Integration
	3. Reduction / Scaling
6. Store it.

Relational databases are the easiest to 'wrangle' because of their defined schemas



## Preprocessing
Assume the data has been extracted and saved
Often in various formats
Could be missing data

Preprocessing makes *data consistent*


### Assessing Data Quality
- Accuracy
	- Correct or wrong, accurate or not
- Completeness
	- Is it recorded/available?
- Consistency
	- Discrepancies in representation
- Timeliness
	- Updated in a timely way
- Believability
	- Do I trust the data is true?
- Interpretability
	- How easily can I understand the data?


### Rescaling Numerical Data:
- Normalisation:
	- Rescale the values to be 0 and 1
	- Use when the numbers have different units (inches, cm, etc.)
	$$\frac{(x-x_{min})}{(x_{max}-x_{min})}$$
- Standardisation:
	- Scales the model using mean and standard deviation
	- Useful when the data is on the same scale
	- We want to set the mean to 0 and standard deviation to 1

- Other rescaling transformations:
	- $x^k$, $log(x)$, $e^x$, $|x|$, $\frac{x1}{x2}$
	- This is useful for *feature engineering*
	- Helps you 'warp the dimensions' of your data space
	- (Not always appropriate)
