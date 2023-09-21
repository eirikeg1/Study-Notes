# History
---
## Predominant approaches
### Rule-based / knowledge-based 
* 1950-2000
* Explicitly encode linguistic expert knowledge
* Difficult to scale
### Statistic / data-driven / machine-learning
* 1990-today
* machine learning to generalize from annotated data
* Division of labor between annotators / linguists and ML people
*  ![[Pasted image 20230824152106.png | 500]]


## Main NLP tasks
---
#### Natural language generation
* Machine translation
* Question answering
* Grammatical error correction

#### Annotation (natural language understanding)
* Machine translation
* Question answering
* Grammatical error correction
#### The classical NLP pipeline
![[Pasted image 20230824152804.png | 600]]

# Data preparation
---
_The data should be prepared so the algorithm can use it. It is important to make sure the same preprocessing is applied to all datasets_
#### Data preprocessing
* Remove unwanted elements (empty lines, HTML tags...)
* Split text into sentences (or what you want)
* Tokenize
* Case folding (make words non-case sensitive)

#### Feature extraction
* Define instance scope (word, sentence)
* Define features and their types
* Extract feature values from data

**Typical dataset example:**
![[Pasted image 20230824152913.png | 500]]

**Another example:**
![[Pasted image 20230824153009.png | 500]]

### Data preprocessing
---
#### Sentence splitting
* Split after _.?!_
* Difficulties / corner cases?
	* Abbreviations like _Mr._ or _U.S.A_
	* What about Abbreviations at the end of a sentence?
	* Is the colon a sentence boundary?
	* Typos or bad formatted data (like on social media)
* Example with NLTK:
	* ![[Pasted image 20230824154558.png | 250]]
	* sent_tokenize provides language-specific models
* Sentence splitters are mostly rule-based (regular expressions)

#### Tokenization
* How many tokens in the following sentence?
	* _For example, this isn't a well-formed example_
* Tokenization is mostly a matter of conventions, and case specific
* Example with NLTK:
	* ![[Pasted image 20230824154921.png | 250]]
	* Uses the Punk tokenization model for English, but there are also even simpler tokenizers based on regular expressions

#### Case folding
* Should _The_ be different from _the_
* How about _apple_ and  _Apple_
* Simplest solution is to convert everything to lowercase
* **Truecasing:** 
	* Count how often each word appears lower cased and how many times capitalized in a document (or what you want to consider)
	* Choose the most frequent count

### Feature extraction
---
#### Counting words
_In large corpuses of text we can count words, characters, word sequences and more in order to get better results_

* **By having a count of things like this we can for example:**
	* Compare different corpora with each other
	* Discover statistical regularities (frequency laws)
	* Build statistical models that can generate new texts and classify existing texts
* Results are based on the preprocessing
* Example of a frequency distribution from _Tom Sawyer_:
	* ![[Pasted image 20230824160223.png]]
* Words that only occur once in a text are called **hapax legomena** (or **hapaxes**)

#### Lexical diversity
* **Tokens**: number of words in running text (with repetition)
* **Types**: number of unique words in running text
	* _one cat caught five mice and three cats caught one mouse_ → 11 tokens, 9 types
	* **Type-token ratio (TTR)**: types / tokens, expressed in %
		* 81.8% for the example sentence 
		* TTR is a measure of lexical diversity 
		* Which type of text has higher TTR, a newspaper article or a transcript of an informal conversation?

**Collocations**
_A sequence of words that occur together unusually often_

#### Zipf's law
_The product of the frequency of a word f and its position in the frequency list (rank) r is constant_
* _f_ ∙ _r_ = _k_
* The first word is twice as frequent as the second, the first is three times as frequent as the third and so on
* The number of meaning of a word is correlated with it's frequency
* The length of a word is inversely correlated with it's frequency
* Words tend to clump together in a text

**The law only holds approximately**:
* Unstable behavior for most frequent words
* Large variation for least frequent words
* The constant (slope of the regression line) differs according to language and data type

**Practical implications**:
* Almost all words are rare
* Whatever the size of the corpus, many words occur only once, and many will not appear at all

**Visualizations**:
![[Pasted image 20230824161512.png | 750]]

**Is not only reasonably accurate for English**:
![[Pasted image 20230824162159.png | 500]]

**The same can be said when looking at numerals ("one", "two",...)**
![[Pasted image 20230824162247.png | 500]]