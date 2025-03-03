

## Categories of data formats


| Unstructured | Semi-structured | Structured  |
| ------------ | --------------- | ----------- |
| Text file    | CSV             | Database    |
| Audio        | Webpages        | Spreadsheet |
| Video        | XML             |             |
|              | JSON            |             |

Unstructured data is typically more *human readable*
Structured data is typically more *machine readable*



### CSV:
- Tabular comma separated values
### HTML:
- Tags are keywords contained in angle brackets
- Tags are *not case sensitive*

### XML:
- Generalised markup language
- Allows completely custom tags
- Some General Rules:
	- Must have a **single root element**
	- All opened tags must be closed
	- Case sensitive
	- '<' and '&' are illegal inside an element
	- Must have a version declaration at the beginning

```XML
<?xml version="1.0"?>
<cities>
	<!-- Example of storing a city -->
	<city>
		<name>Melbourne</name>
		<state>Victoria</state>
	</city>
	
	<!-- Using attributes -->
	<city name="Melbourne" state="Victoria"/>
</cities>
```

### JSON:

Loading JSON into Python objects:
```python
import json

with open("filename.json", "r") as json_file:
	json_obj = json.load(json_file)
	# Done!
```

#### Exercise:
```json
person: {
	firstName: "Homer",
	lastName: "Simpson"
}
```



## Metadata
Almost every data item stands for something outside of the program

In addition to data **format**, data has a **semantic type**
- The type represents the meaning of the data in the world
- Knowing the type of data helps you understand what computations make sense
- The mapping to a world object or concept is called its *denotation*


Large programs or databases may have hundreds of different semantic types of data
- They may all be the same syntactic type / format
- E.g. salary, height, age, number of children are all numbers, but with different semantic meaning

For recordkeeping, you use a *metadata schema*: a list or structure of all the types with their definitions and restrictions.
- **Data about data**

### Knowledge Graphs
- Represents the world

![[knowledge-graph.png]]