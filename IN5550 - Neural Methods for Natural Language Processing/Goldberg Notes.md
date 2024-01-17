
# Chapter 1
---

* Human language is highly ambiguous: *I ate pizza with friends* compared to *I ate pizza with olives*
* In contrast to computer vision where you can use mathematically formulas to go from one color to another (for example from a red to its respective greyscale counterpart), there are no such formulas for natural language (from red to pink for example), would potentially need huge lookup table

## Different types of networks

* **Classic Feed Forward Networks** are good at detecting patterns in fixed size or variable length inputs, disregarding the word order
* **Convolutional Neural Networks** are specialized in extracting meaningful local patterns that are sensitive to word order
	* Convolutional layers can help model pick up on local patterns
* **Recurrent Neural Networks** are specialized for sequential data. Can be used for language generation
* **Recursive Networks** extends **RNN**s from sequences to trees. 
