# The Jewish Bookshelf Project (JBS)
In the JBS project we build a RDF [Linked Dataset](https://en.wikipedia.org/wiki/Linked_data) for the *Jewish bookshelf* (JBS). The project consists of the following major efforts:
- Defining a JBS [ontology](https://en.wikipedia.org/wiki/Web_Ontology_Language).
- Representating the *structure* of various Jewish texts in RDF format, based on the defined ontology.
- Conducting a *text analysis* tasks on the texts, and representing the results also in RDF.

# The JBS ontology
We list here the principles guiding the definition of the JBS ontology.
- Each Jewish book is associated with a specific *class*. Example classes are: *Tanach*, *TalmudBavli*, and *Mishna*.
- Additional classes such as Halacha (הלכה) and Machashava (מחשבה) represent book categories.
- Internal book elements are also denoted as classes, e.g., Pasuk, Perek, Parasha.
- Key properties
  - *within*. Denotes that subject s1 is contained within subject s2, e.g., that a subject of type *Pasuk* is contained within a subject of type *Parasha*.
  

# Input RAW Texts
The RAW texts used in the projects are currently extracted from the following web sources:
- [Torat Emet](http://www.ateret4u.com/online/a_root.html) website.
- The [Sefaria](https://github.com/Sefaria/Sefaria-Export) archive.
Both sources distribute their texts with open licenses.

# Structural RDF representation
We have built software tools to analyze the raw texts and represent the resulting elements in RDF format.

