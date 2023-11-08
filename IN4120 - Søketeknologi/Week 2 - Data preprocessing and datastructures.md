
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
**Synonyms/homonyms:*
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
* Website often start with: https or www etc.

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

# String data structures and algorithms
---
## Sorted arrays:
* Allows binary search
## Skip pointers/skip lists
* Some entries has pointer pointing further up, when searching check if you can _skip_

**Where to place skip pointers?**
* Depends on data
* More skips -> shorter skip spans -> more likely to skip
* Fewer skips -> few comparison, but long skip spans -> few successful skips
* Presence of book keeping can hurt caching on modern hardware, unless you're memory-based
* Common way:
	* for postings of length L, use √L evenly-spaced skip pointers
	* This ignores distribution of query terms
	* Easy if index is relatively static 

![[Pasted image 20230830113240.png | 500]]

## Tries:
* Tree data structure
* Good for prefix matching
* Search for words character (or token) by characters
* Usually stored as a big continuous buffer (bytes)
* A lot of words have shared both prefixes and suffixes, word 
* Usually also stores end of word nodes
* **Trie stored in a buffer representation:**![[Pasted image 20230830115716.png | 750]]
## Suffix arrays
* A prefix of a suffix is an infix
* Represent a suffix as an integer offset into the original string (to expensive to store new duplicate strings)
* Sort lexicographically
* Sorted list of integers is the **Suffix Array**
* Use binary search to locate matching substrings
![[Pasted image 20230830120227.png | 500]]

**Can include starting position values:**
![[Pasted image 20230830120401.png | 500]]

**If you use transformations first you can get an inverse algorithm:**
* We still use these after Burrows-Wheeler transform
![[Pasted image 20230830120530.png | 500]]

# Burrows-Wheeler Transform
_Make strings more compressible by making them easier to run-length encode_

* Transforms one string to another one and then back
* The new string has a lot of duplicates which makes it simpler to compress
* ![[Pasted image 20230830115927.png | 500]]


# Edit Tables
_Table used to compute and represent the edit distance between strings_

* Can be useful for typing errors

![[Pasted image 20230906105130.png | 500]]

### Edit distance
_The smallest number of edit operations needed to rewrite one string into another__

* Minimal edit sequence is not unique, depends on implementations and perspectives
* Can be generalized to finding minimal edit costs 
* *Levenshtein distance* is an example of edit distance

### Edit operations
* Insert:
	![[Pasted image 20230906104656.png| 300]]
* Delete
	![[Pasted image 20230906104725.png | 300]]
* Replace
	![[Pasted image 20230906104744.png | 300]]
* Transpose:
	![[Pasted image 20230906104803.png | 300]]

### Computing values
* Damerau-Levenshtein update rule
* Start at the NW-most corner
* Answer is in the SE-most corner
	![[Pasted image 20230906105343.png | 500]]

### Speedups
* Assuming unit edit costs we can represent an edit table using four bit vector, encoding vertical/horizontal positive/negative differences between table cells
* Speedups proportional to machine word size!
* Extensions exist that allow multiple strings to be packed into the same machine word
![[Pasted image 20230906105806.png | 500]]
* Words with same prefixes can share pars of table
	![[Pasted image 20230906110007.png | 500]]



# Tries and edit tables

* Organize dictionary in a trie
* Keep track of depth when traversing trie
* Reuse parts of the edit table
	* Only on column to update
* Prune the search space early
	* Make assumptions (first character is always correct etc.)
	* Abort traversal when edit threshhold is exceeded


# The Aho-Corasick Algorithm
_Efficiently find all strings in a given buffer that also appear in a huge dictionary_

* In practice a trie with some extra edges
* Search for all strings simultaneously, dictionary size does not matter
* Kind of like a "trie walk"
* The application dictates where matches can begin and end
* Can be combined with basic NLP to find linguistic variants