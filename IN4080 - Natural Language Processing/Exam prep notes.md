
## Sequence labeling

* **Entity**: name or place which can span over multiple words (*San Fransisco*)
* **BIO-encoding**
	* Beginning, inside or outside an entity
	* One tag per word
* **Viterbi**
* 

### Naive Bayes

Dealing with rare words:
* Smoothing
* Rare words class


## Dialogue systems

### Dialoge systems

* Basic architecture
	1. user gives input signal
	2. Language understanding in a representation of user intent
	3. Generation/response selection
* Turn taking
* Dialoge acts
	* Each utterance is an action performed by speaker
		* Speaker has specific goal
		* Speaking triggers effects
* Searle's Taxonomy
	* Assertives
	* Directives
	* Commissives
	* Expressives
	* Declaratives
* Deixis
* Grounding
	* Grounding acts
		* Backchannels
		* Explicit feedback
		* Implicit feedback
		* clarification strategies
		* Repair strategies
* Conversational implications
* Alignment

#### Dialogue models

* Intent recognition
	* LLMs classifuing input as action/intent
* Slot filling
	* Sequence labeling task
* Transfer learning (fine tune pre trained models)
* Data augmentation 
	* Synthetic data
	* Generate new labelled utterances from existing ones, using small changes
	* Translate to multiple languages, maybe translate back as well
	* New formulations

### Dialogue with language models

* Beam search (for decoding)
	* Store possible next token in a tree structure with the probabilities
	* Instead of choosing next greedily, take the path with highest probability $k$ steps forward
* Retrial-augmented models
	* Retriever and generator
* Fine tuning
	* In context learning
	* Parameter efficient fine tuning (PERT)


### Speech/audio processing

* Convert signal to spectrogram
* Disfluencies
	* Pauses, fillers ('um', 'liksom')
	* Repetitions
	* corrections ('the ball, err mug')
	* Repairs ("the bu/ball")


### Handcrafted dialogue systems

* Finite state automata
	* Flow chart representing input to actions
* Frame based managers
	* Questions with 'slots' (for example time or location) to be filled by the user
	* For every user utterance fill all possible slots then ask for the remaining slots

### Markov Decision Process

* 