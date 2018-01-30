# The Jewish Bookshelf Project (JBS)
In the JBS project we build a [Linked Dataset](https://en.wikipedia.org/wiki/Linked_data) for the *Jewish bookshelf* (JBS-LD). The project consists of the following major efforts:
- Defining a JBS ontology (classes and properties).
- Representating the *structure* of various Jewish texts in RDF format, based on the defined ontology.
- Conducting *text analysis* tasks, and representing the results in RDF. Current main task is detecting quotations of Bible verses (psukim) in a given text.

*You comments and suggestions are welcome and should be directed to Oren Mishali (omishali at cs.technion.ac.il).*

# The JBS ontology
The current (and evolving) version of the ontology is available [in ttl format](https://github.com/TechnionTDK/jbs-json23plet/blob/master/ontologies/ttl/JbsOntology.ttl). You may also be interested to explore the JBS ontology (and the whole dataset) using a visualization tool that we have developed called [eLinda](http://tdk-p6.cs.technion.ac.il:8081/?graph=jbs.technion.ac.il&languages=&endpoint=tdk3.csf.technion.ac.il:8890/sparql).

## About the ontology
PREFIX jbo: \<http://jbs.technion.ac.il/ontology/>  
PREFIX jbr: \<http://jbs.technion.ac.il/resource/>

We view the Jewish Bookshelf as a collection of books. Each book inserted to the JBS-LD is given a unique URI (e.g., *jbr:book-tanach*), and a class type *jbo:Book* (via *rdf:type* property). We view each book as having a tree hierarchy, where the "leaves" of the tree (the lowest level) are its text elements (i.e., text found within a chapter or within a section). For example, in the Tanach (Bible) each text element is a single verse (pasuk). Each text element is given a URI, and a class type *jbo:Text*. Other elements of type *jbo:Section* represent the chapters or sections themselves where the text elements are contained. Note that text elements are the only elements that point to the actual text content (via a *jbo:text* property). Other useful properties of text elements are *jbo:position* (numerical ordering within the book), *jbo:book* (a pointer to the containing book), and *rdfs:label* (a short human-readable description).

# The basic workflow
The JBS workflow begins with raw Jewish texts and ends with RDF triples ready for consumption. Following are the key workflow components:
- [jbs-raw](https://github.com/TechnionTDK/jbs-raw) is the repository where the raw texts reside. The raw texts are extracted from the following open-licensed web sources:
  - [Torat Emet](http://www.ateret4u.com/online/a_root.html) website.
  - The [Sefaria](https://github.com/Sefaria/Sefaria-Export) archive.
- The raw texts are then analyzed and turned into structured json files. The analysis is made using a library we have developed called [text2json](https://github.com/TechnionTDK/jbs-text2json), and the output jsons reside in the [jbs-text](https://github.com/TechnionTDK/jbs-text) repository.
- The jsons in jbs-text are turned into rdf (ttl) format using a tool we have developed called [json23plet](https://github.com/TechnionTDK/jbs-json23plet).
- The ttl files are loaded into a Virtuoso server. The Virtuoso endpoint is available at http://tdk3.csf.technion.ac.il:8890/sparql.

If you use the endpoint (via SPARQL) don't forget to set the name of the graph to http://jbs.technion.ac.il. The following example query will return all book triples:

```
PREFIX jbo: <http://jbs.technion.ac.il/ontology/>
PREFIX jbr: <http://jbs.technion.ac.il/resource/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
SELECT * WHERE {
  ?s ?p ?o.
  ?s a jbo:Book.
}
```

# Text analysis

