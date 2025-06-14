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

We chose the Basilica di Santo Stefano as our first topic. Then, we examined the ArCo ontology to see to which class the churches belong. We found two classes: a more general one (arco:ImmovableCulturalProperty) and a more specific one (arco:ArchitecturalOrLandscapeHeritage). We chose ImmovableCulturalProperty. Then we did the first query in order to find the Basilica di Santo Stefano on ArCo, and we also employed the keyword DISTINCT to be sure not to have any duplicates in the results.

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

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

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

[back](./)
```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
