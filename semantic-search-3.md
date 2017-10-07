# Information Retrieval via SemanticSearch on LinkedData

This blog is continuation of [part2](https://spoddutur.github.io/my-notes/semantic-search-2).. So far, we have covered:
1. How traditional keyword search works and how it falls behind in capturing user intent
2. The challenges for semantic search
3. Solution1 - How to capture user intent

In this blog, we are going to discuss a more generic solution for capturing user intent

## 4. Solution2 - A more generic approach for capturing user intent
In earlier method, for a given set of words in user query, we relied on WordNet vocabulary to add synonyms and generate expanded query. In this method, we don't rely on any such dictionary.

## 4.1 Generic Query Expansion via Mapping keywords to LinkedData Resources
As the title suggests, in this generic method, to expand query we map user keywords to linkeddata resources and get its corresponding semantic synonyms from owl:class and rdf:property labels of the Dataset.

## 4.1.1 Algorithm to get semantic synonyms:
For every keyword w in user query, if an entity E exists for w in Dataset, then to get its semantic synonyms, explore the neighbours N of E such that:
- N is of type owl:class or rdf:property
- N is related to entity E via predefined Labelling relations.
- **Labelling relations =** {rdfs:Label, owl:sameAs, foaf:name, dc:title, rdfs:subClassOf, skos:prefLabel, skos:altLabel, rdfs:range, dbo:product, rdf:type}

### 4.1.2 Example:
The below picture illustrates how this computation happens for user query Honda. Pick the neighbours who are related to Honda through one go the labelling relations. Result: Automotive, organisation, vehicle and engine as semantic synonyms.
![image](https://user-images.githubusercontent.com/22542670/31304227-adc2ba42-ab3a-11e7-9acc-665e1f7be381.png)

### 4.1.3 Some more examples:
UserQuery and its corresponding semantic synonyms:
- *honda*: dbpedia-owl:automotive, dbpedia-owl:organisation, dbpedia-owl:vehicle and dbpedia-owl:engine
- *spacecraft*: dbpedia-owl:spacecraft, dbpedia-owl:satellite, dbpedia-owl:missions and dbpedia-owl: Rocket
- *wife*:	dbpedia-owl:spouse, dbpedia-owl:person, dbpedia-owl:family and dbpedia-owl:sex
- *bass*:	dbpedia-owl:fish, dbpedia-owl:instrument, dbpedia-owl:note and dbpedia-owl:musical

## 5. Conclusion: 
This generic approach uses semantic similarity to expand query. These expanded sets are more general than ‘synsets’ (sets of synonyms within dictionary-oriented terms) in both scope, including a huge potential range of named entities, and in the flexibility of the semantic relationships covered.
**Hybrid approach:** In general, a multi-strategy approach is recommended where this generic approach is used only after the lexical expansion with WordNet failed to give desired result.

## References:
- [http://dbpedia.org/page/Honda](http://dbpedia.org/page/Honda)
- [https://www.redlinels.com/hypernyms-and-hyponyms/](https://www.redlinels.com/hypernyms-and-hyponyms/)
- [https://www.thoughtco.com/what-is-a-meronym-1691308](https://www.thoughtco.com/what-is-a-meronym-1691308)
- [https://www.thoughtco.com/what-is-a-meronym-1691308](https://www.thoughtco.com/what-is-a-meronym-1691308)
- [http://thescipub.com/PDF/jcssp.2015.361.371.pdf](http://thescipub.com/PDF/jcssp.2015.361.371.pdf)
- [http://ceur-ws.org/Vol-992/paper3.pdf](http://ceur-ws.org/Vol-992/paper3.pdf)