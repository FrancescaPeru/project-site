---
layout: default
---

# INDEX

1. [Methodology](#1-methodology)
   
2. [Immovable Cultural Property _Basilica di Santo Stefano_](#2-immovable-cultural-property-basilica-di-santo-stefano)
   
3. [Immovable Cultural Property _Basilica di San Petronio_](#3-immovable-cultural-property-basilica-di-san-petronio)

## 1. Methodology

* Making hypotheses

* Looking for the data in the ArCo ontologies documentation: http://wit.istc.cnr.it/arco/

* Realizing queries using the ArCo SPARQL endpoint: https://dati.cultura.gov.it/sparql

* Verifying if the retrieved data could actually back up our hypotheses or not

* Using Large Language Models 

* Creating RDF triples that could be addeded to the knowledge graph

## 2. Immovable Cultural Property _Basilica di Santo Stefano_

### Step 1

We chose the Basilica di Santo Stefano as our first topic. Then, we examined the ArCo ontology to see to which class the churches belong. We found two classes: a more general one (arco:ImmovableCulturalProperty) and a more specific one (arco:ArchitecturalOrLandscapeHeritage). We chose ImmovableCulturalProperty. Then we did the first query in order to find the Basilica di Santo Stefano on ArCo, and we also employed the keyword **DISTINCT** to be sure not to have any duplicates in the results.

```js
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX arco: <https://w3id.org/arco/ontology/arco/>

SELECT DISTINCT*
WHERE {
?s a arco:ImmovableCulturalProperty; 
rdfs:label ?label.
FILTER (?label, "Basilica di Santo Stefano", "i") 
}
```
We obtained 0 results.

### Step 2

Since we did not get any results, we made the query more generic by looking for an Immovable Cultural Property related to “Santo Stefano” in the city of “Bologna”. In order to do so, we used the keywords **FILTER** and **REGEX** to obtain results containing these substrings. 

```js
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX arco: <https://w3id.org/arco/ontology/arco/>
PREFIX dc: <http://purl.org/dc/elements/1.1/>

SELECT DISTINCT*
WHERE {
?cp a arco:ImmovableCulturalProperty;
rdfs:label ?label;
dc:coverage ?coverage.
FILTER(
REGEX(?label, "santo Stefano", "i") &&
REGEX(?coverage, "Bologna", "i"))
}
```
We obtained 0 results.

### Step 3

Still not obtaining any results, we decided to base our research on the address “Piazza Santo Stefano” in order to find the buildings located there. We asked the LLMs to write a query to retrieve this information with the **prompting technique chain-of-thought**. 

AGGIUNGERE FOTO LLMS CHAIN OF THOUGHT RISULTATI

Analysing the LLMs results we noticed that:
* Mistral did not use ArCo’s properties and did not filter the label;
* Gemini did not filter the label;
* ChatGpt correctly used ArCo’s properties that we provided and used the double FILTER to find the square in Bologna.

Using the ChatGpt’s query, we obtained this IRI as a result [IRI address Piazza Santo Stefano](https://w3id.org/arco/resource/Address/4e1342b28cd0daeca522227839eef00c)

After reviewing the results and knowing that the _Basilica di Santo Stefano_ is a complex of churches, we noticed that there is no entity representing the Santo Stefano complex as a whole, but the various churches that form the Basilica are listed separately.

#### SUGGESTION 

To enrich ArCo, it would be useful to add a single entity that represents the entire complex with its own IRI and to link it to the corresponding entity on DBpedia [IRI DBpedia Basilica di Santo Stefano](https://dbpedia.org/resource/Santo_Stefano,_Bologna) by using the property owl:sameAs.

### Step 4

Among the churches in Piazza Santo Stefano that form part of the Basilica, we choose _Chiesa del Crocifisso_, and by analyzing its RDF page, we noticed that among the missing information there is the saint to whom it is dedicated.

We asked the LLMs to find the saint to whom the Chiesa del Crocifisso is dedicated with the zeroshot prompting technique. According to our investigations, we discovered that it is dedicated to San Giovanni Battista.
* Question: To whom is dedicated Chiesa del Crocifisso in Piazza Santo Stefano in Bologna?

INSERT FOTO

Result: Gemini answered correctly with “San Giovanni Battista” while both Mistral and ChatGpt provided wrong answers.

### Step 5

We wrote a query in order to find the IRI of San Giovanni Battista on ArCo. We also employed the keyword **ORDER BY ASC **to have more organized results.

```js
PREFIX cpv: <https://w3id.org/italia/onto/CPV/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
SELECT DISTINCT*
WHERE {
?agent a cpv:Person;
rdfs:label ?label
FILTER(REGEX(?label, "Giovanni Battista", "i"))
}
ORDER BY ASC (?label)
```
We are provided with hundreds of results that don’t match with the entity that we were looking for.

#### SUGGESTION

To enrich the knowledge graph it would be useful to create an IRI in ArCo to identify San Giovanni Battista.
We imported from dbpedia the IRI of San Giovanni Battista to enrich ArCo’s knowledge graphs with a new entity [IRI DBpedia Giovanni Battista](https://dbpedia.org/page/John_the_Baptist).

#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

[Link to home](./linktohome.md)
[back](./)
```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
