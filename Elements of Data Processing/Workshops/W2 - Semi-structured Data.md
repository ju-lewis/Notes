

Relevant libraries for Python JSON and XML processing:
```python
import json
from lxml import etree
```


## Manipulating XML Trees:

Opening an XML file and reading into a tree-like structure:
```python
xml_tree = etree.parse("sample_xml.xml")


"""
Useful attributes / methods
"""
root = xml_tree.getroot()
print(root.tag) # Gets the tag name (e.g. cinema for <cinema>)
print(root.attrib) # Gets all attributes as a dict
print(root.text) # Gets text within the tag (not nested!)
print(len(root)) # Gets the number of child elements
print(root.get("attribute_name")) # Gets a specific attribute
```

We can index the immediate children of an element as you would index a list:
```python
first_child = root[0] 
```

Or you can get the first element matching a tag name:
```python
first_movie = root.find("showings")


# We can also iterate over all matching children!
for movie in root.iterchildren(tag = "showings"):
	print(movie.attrib)

# You can also recursively search the tree for matching tags:
for date in root.iterdescendants(tag = "date"):
	print(f"Showing date: {date}")
```

We can add to the XML tree using `append`:
```python
root.append(etree.Element("showings"))
```


Finally, writing XML to a file can be done as so:
```python
# Recreate entire tree structure from just the root node
new_tree = etree.ElementTree(root)

# Note the 'write binary' access mode.
with open("output.xml", "wb") as fp:
	new_tree.write(fp, xml_declaration=True)
```

## Manipulating JSON Objects

Loading:
```python
import json

# Load from file
json_dict = json.load("filename.json")

# Load from string
other_json_dict = json.loads('{"example": ...}')
```



