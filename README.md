# The Jewish Bookshelf Project (JBS)
In the JBS project we build a [Linked Dataset](https://en.wikipedia.org/wiki/Linked_data) for the *Jewish bookshelf* (JBS-LD). The project consists of the following major efforts:
- Defining a JBS ontology (classes and properties).
- Representating the *structure* of various Jewish texts in RDF format, based on the defined ontology.
- Conducting *text analysis* tasks, and representing the results in RDF. Current main task is detecting quotations of Bible verses (psukim) in a given text.

```
You comments and seggestions are welcome and should be directed to **Oren Mishali** (omishali at cs.technion.ac.il).
```

# The JBS ontology
The current (and evolving) version of the ontology is available [in ttl format](https://github.com/TechnionTDK/jbs-json23plet/blob/master/ontologies/ttl/JbsOntology.ttl). You may also be interested to explore the JBS ontology (and the whole dataset) using a visualization tool that we have developed called [eLinda](http://tdk-p6.cs.technion.ac.il:8081/?graph=jbs.technion.ac.il&languages=&endpoint=tdk3.csf.technion.ac.il:8890/sparql).

## About the ontology
PREFIX jbo: \<http://jbs.technion.ac.il/ontology/>  
PREFIX jbr: \<http://jbs.technion.ac.il/resource/>

We view the Jewish Bookshelf as a collection of books. Each book inserted to the JBS-LD is given a unique URI (e.g., *jbr:book-tanach*), and a class type *jbo:Book* (via *rdf:type* property). We view each book as having a tree hierarchy, where the "leaves" of the tree (the lowest level) are its text elements (i.e., text found within a chapter or within a section). For example, in the Tanach (Bible) each text element is a single verse (pasuk). Each text element is given a URI, and a class type *jbo:Text*. Other elements of type *jbo:Section* represent the chapters or sections themselves where the text elements are contained. Note that text elements are the only elements that point to the actual text content (via a *jbo:text* property). Other useful properties of text elements are *jbo:position* (numerical ordering within the book), *jbo:book* (a pointer to the containing book), and *rdfs:label* (a short human-readable description).


# Input RAW Texts
The RAW texts used in the projects are currently extracted from the following web sources:
- [Torat Emet](http://www.ateret4u.com/online/a_root.html) website.
- The [Sefaria](https://github.com/Sefaria/Sefaria-Export) archive.
Both sources distribute their texts with open licenses.

# Structural RDF representation
We have built software tools to analyze the raw texts and represent the resulting elements in RDF format.

