
# Challenges of Natural Language Processing
---

* Human language is highly ambiguous: *I ate pizza with friends* compared to *I ate pizza with olives*
* In contrast to computer vision where you can use mathematically formulas to go from one color to another (for example from a red to its respective greyscale counterpart), there are no such formulas for natural language (from red to pink for example), would potentially need huge lookup table

# Different types of networks
---

## Classic Feed Forward Networks 

* Are good at detecting patterns in fixed size or variable length inputs, disregarding the word order
* [[Week 7 - Neural networks#Feed forward neural networds|Explanation from IN4080]]

## Convolutional Neural Networks 

* Are specialized in extracting meaningful local patterns that are sensitive to word order
* Convolutional layers can help model pick up on local patterns

## Recurrent Neural Networks 

* Are specialized for sequential data. Can be used for language generation
* Takes a sequence of items as input and returns a fixed size output which _summarizes the sequence_, which can mean different things in different contexts
* Are rarely used as a standalone network, often fed into other networks as input
* Allows for abandoning [[Week 5 - Sequence labeling 2#Trick 2 The Markov Assumption |The Markov Assumption]]
* Networks with **convolutional** and **pooling** layers are useful for classification tasks in which we expect to find strong local clues regarding class membership
* Recurrent and Recursive Networks allow working with sequences and trees while preserving a lot of the structural information, which is good when learning regularities in structured data of arbitrary sizes

## Recursive Networks 

* Extends **RNN**s from sequences to trees. 
* Useful as many of the problems in NLP are structured, requiring the production of complex output structures
* 