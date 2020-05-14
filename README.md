# EUR-Lex Python

## a simple Python library for EUR-Lex

The primary purpose of this library is to identify components of the documents available through EUR-Lex.

EUR-Lex documents are described using the FRBR Work/Expression/Manifestation/Item vocabulary. The `query` function in this library returns an iterable of Work objects, each of which provides information about a document, its expression, and all of its manifestations and items. 

It requires registration credentials with the EUR-Lex Webservice. Any expert search is permitted; by default queries are limited to the Legislation collection (DTS = 3).

English document is selected by default. But the language can be changed by selecting a two-position isocode as optional parameter.

For example, the following code prints information about each item:

```python
from eurlex import EUR_Lex

for work in EUR_Lex.query(username, password):
    print()
    print('CELEX:', work.celex)
    print('type:', work.type)
    print('year:', work.year)
    print('number:', work.number)
    print('date:', work.date)
    exp = work.english_expression
    print('  language:', exp.language)
    print('  title:', exp.title)
    for manifest in exp.manifestations:
        print('    format:', manifest.format)
        for item in manifest.items:
            print('      uri:', item.uri)
            print('      filename:', item.filename)
```
If you want to execute an expert search query for a selected language, you need to proceed as follow; 

```python
from eurlex import EUR_Lex

for work in EUR_Lex.query(username="username", password="password", q="DN = 32015R0062", lg="fr"):
    print()
    print('CELEX:', work.celex)
    print('type:', work.type)
    print('year:', work.year)
    print('number:', work.number)
    print('date:', work.date)
    exp = work.lg_expression
    print('  language:', exp.language)
    print('  title:', exp.title)
    for manifest in exp.manifestations:
        print('    format:', manifest.format)
        for item in manifest.items:
            print('      uri:', item.uri)
            print('      filename:', item.filename)
```			
For the selection of language or the expert search query mode, see https://eur-lex.europa.eu/content/help/faq/intro.html
