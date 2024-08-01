
## Numerical Data:
- Countable => discrete (year, )
- Not easily countable => continuous (share price, people in city, temperature, etc.)

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



