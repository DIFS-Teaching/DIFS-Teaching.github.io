# Intelligent extraction

That is, without ``manual work'' in the form of searching for elements, regular expressions, CSS selectors, XPath expressions, etc.

1. Machine learning
	- Manually annotated examples of web pages
	- The wrapper/extractor parameters are automatically derived from them
2. Model-driven extraction
	- Specification of the expected data structure
		- Entities, attributes, relationships (ER diagram?)
		- Method of recognizing individual attributes
	- Finding the occurrence of the required data groups in the source page

---

# Machine learning scenario

- Training set of documents
	- Usually documents from a single source
	- Annotation of the parts of the content to be extracted
	- Deriving extraction rules
- A set of new, unknown documents
	- Data extraction based on derived rules

---

# Machine learning -- methods

- Sequential page models (characters, tokens)
	- Grammar inference (*wrapper induction*), hidden Markov models, ...
- Hierarchical models
	- Generalized DOM (removal of implementation details)
	- Tree automata
- Visual document models
	- Page segmentation
	- Classification based on visual features

---

# Model-driven extraction

![ERD](assets/erd.png) <!-- .element: style="float:right;height:700px" -->

- Input: Entities, attributes, relationships
- Approximate recognition of individual data fields
	- Regular expressions
	- Classification of text or visual properties
	- Mapping to a knowledge base (DBPedia, ...)
- Finding data records
	- Exploiting regularity, repeating patterns
