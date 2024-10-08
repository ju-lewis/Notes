## Intellectual Property
Using digital content without permission is stealing
- Enforced by law

### IP Control
**Patent**: The right granted by the government to an *inventor*, giving the owner the right to exclude others from making, using, selling, offering to sell, and importing an invention for a *limited period of time*

**Copyright**: Preventing an original *work* to be copied or used, except by the creator who has exclusive rights

**Trademark**: A recognisable *sign or logo*, a design that distinguishes a trader's products

**Trade Secret**:


### Your Responsibility
All data scraping and crawling must be done legally and ethically (this is the responsibility of the bot creator)

### Open Data Commons Licences
**Public Domain Dedication and License (PDDL)**: Dedicates the database to the public domain. Completely unrestricted use.

**Attribution License (ODC-By)**: Free to use, but must be accompanied by an attribution

**Open Database License (ODC-ODbL)**: Must provide free access of the product to the data owners. Must be distributed under the same license.


### Creative Commons Licenses
**CC0**: Owners waive their copyright rights

**CC-BY**: Attribution license

**CC BY-SA** Attribution-ShareAlike, users must give credit and distribute under the same license.


### Copyright
Copyright holds as soon as you make an image or text

If you download someone's *image* you must use attribution (unless given written permission)
If you repeat for than $N$ words of someone's *text* you must use attribution


## Privacy

### Public Data Release and Anonymity

*Terminology*:
- Quasi-identifier: the columns which we're trying to identify a person by
	- *e.g.* Age, hair colour, gender, etc.
- Sensitive attribute: The attribute we're trying to connect an individual to
	- *e.g.* COMP20008 grade


**k-anonymity** is satisfied if every record in the table is indistinguishable from at least $k-1$ other records
- For example *3-anonymous* implies  there are at least 3 identical records for any given record in the dataset; if there are any fewer, then the k-anonymity is reduced.

**l-diversity**: For each $k$ anonymous group, make sure there are at least $l$ different sensitive attribute values.
- Takes the *minimum* value of the dataset 
- Very difficult to achieve


Typically we combine some degree of $k$-anonymity and $l$-diversity



## Bias

