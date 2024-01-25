* More data preprocessing at [[Week 1 - Introduction and data preparation]]
# Parsing
---
* What format/language?
* What character set? (UTF-8,...)

## Tokenization
* Hyphens?
* Double words
* Languages?
	* Different rules and formats, switch direction mid way

#### Stop words
* Words with little meaning to not save in postings
* Trend now is to keep them, as compression reduces storage problem
* Can be important for phrases like _flights to London_

#### Normalization
* Key goal: How are your users like to write their queries for these words?
* Accents
* Dialects 
* Date forms
* Abbreviations across languages? feks _USA_

#### Case folding
* Should _The_ be different from _the_
* How about _apple_ and  _Apple_
* Simplest solution is to convert everything to lowercase

 **Asymmetric expansion**
* Makes search for one word give multiple word results
* ![[Pasted image 20230830110645.png | 500]]

#### Thesauri and Soundex
**Synonyms/homonyms:**
* Save them as both entries?
* For example car/automobile, color/colour

**Spelling mistakes:**
* **Soundex** (forming equivalence classes of words based on phonetic heuristics)

#### Lemmatization
* Reduce inflectional/variant from to base form
* am, are, is → be
* car, cars, car's, cars' → car

#### Stemming
* Reduce terms to their _roots_ before indexing
* automate(s), automatic, automation all reduced to automat
* Is not always real words, but works for indexing

**Porter's algorithm
* Common algorithm for stemming in english
* Conventions + 5 phases of reductions
	* Phases applied sequentially  
	* Each phase consists of a set of commands  
	* Sample convention: Of the rules in a compound command, select the one that applies to the longest suffix
* sses $\rightarrow$ ss
* ies $\rightarrow$ i 
* ational $\rightarrow$ ate

**Other stemmers**
* Lovin's stemmer
* Paice/Husk stemmer
* Snowball
* Full morphological analysis (lemmatization)

**Does stemming help?**
* English: mixed results: helps recall but can harm precision
* Useful for spanish, german, finnish

# Prefix matching
---
# Prefix matching
* Websites often start with: https or www etc.

**Goals**
* Wildcards: search within words or for parts of a word

**General approach**
1. Clever transformation
2. Prefix matching

#### Permuterm indexes and wildcards
_Allows to search for for example h*o (all words which start with h and ends with o)_

![[Pasted image 20230906102638.png | 750]]

**Example of Permuterm rotation**
* Hello -> {hello\$, ello\$h, llo$he,...}
* Dollar sign shows end of actual word
* Often shown with a mar

**After rotations**
Transform wildcard queries into prefix searches over the permuterm vocabulary


**K-gram index**
#NotImportant

	![[Pasted image 20230905125143.png | 500]]

