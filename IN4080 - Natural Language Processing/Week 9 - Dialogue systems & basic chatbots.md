
# Dialogue Systems
---

* An artificial agent designed to interact with humans using natural language
* Can be either text or speech

## Applications
* Chatbots (customer service, chat, ...)
* Mobile virtual assistants
* Smart home
* In car navigation and control
* service robots

## Basic architecture

1. **User** gives input signal (user utterance)
2. **Language understanding** in a representation of user intent (category, embeddings from LLM, etc.)
3. **Generation/response selection**
![[Pasted image 20231017150512.png | 500]]


### Main limitations
* No management of the dialogue itself (beyond local scope)
* better for short interactions

## Architecture with DM

* Keep the state tracking Dialogue management system. Take other context in with the users input signal
* Other messages from the creators to control how the output should be generated
* Can either be done through a customised prompt, or through a logical system. Prompt more modern
* ![[Pasted image 20231017150540.png | 500]]

## What is dialogue
* Spoken/possible non-verbal interactions between two or more participants
* It is an activity serving one or several purposes for the participants

## Turn taking
* Resource allocation problem
* Surprisingly fluid in normal conversations:
	* Minimise both gaps (no speaker) and overlaps more thane one speaker
	* Intervals between speakers is around 250ms
* Turn taking systems tend to be _lazy_ with system waiting for a second pause, makes it more awkward

### Markers for turn boundaries
* Complete syntactic/semantic unit?
* Dialoge structure (greetings -> greetings, question-> answers)
* intonation
* #lecture 

## Dialogue acts
* Each utterance  is an action performed by the speaker
	* Speaker has specific goal
	* Speaking triggers effects

### Searle's taxonomy of speech acts
#toExpand 
* Assertives
	* Commiting the speaker to the truth of a preposition
	* "The exam will take place on November 25"
* Directives
	* Attempts by the speaker to get the addressee to do something
	* "Could you please clean up your room?"
* Commissives
	* Committing the speaker to some future course of action
	* "I promise I'll clean up my room"
* Expressives
	* Expressing the psychological state of the speaker
	* "Thanks for cleaning up your room"
* Declaratives
	* Bringing about a different state of the world by the utterance
	* "You're fired"

## Deixis
* Deixis is dialogue often *referential* to a spatio-temporal context
* The meaning of a deixis depends on the context in the dialogue. 
* Markers:
	* Pronouns (he, her, it)
	* Adverbs of time and place
	* Demonstratives (this, that)
	* Tense markers ("He just left")
	* Others ("the mug to your right", "go away!", "the other one")
	* Non-verbal signs (gestures, pointing, looking)

# Grounding
* Process of gradually augmenting the common ground during the interaction
* Dialogue is a joint collaborative process between participants
* Requires common understanding
* Gradual expansion and refinement of common grounds
* Not just shared common knowledge by participants, but participants know the other person knows
*  Multiple levels
	* Contact
	* Perception
	* Understanding
	* Atitudinal reactions
* ![[Pasted image 20231017193518.png | 250]]

### Grounding acts
* Backchannels: "uh-uh", "mm", "yeah"
* Explicit feedback: "ja det skjønner jeg"
* Implicit feedback: A: "I want to fly to Rome» → B: "there are two flights to Rome on Wednesday: ... »
* Clarification strategies: "Did you mean to Rome or to Goa?», "could you confirm that ...»
* Repair strategies: "OK, you’re not going to Goa. Where do you want to go then?"
	* Strategies to present misunderstandings

# Conversational implications
* Sometimes meaning is sent implicitly:
	* A: "Is he coming to work?" B: "He has a cold"
* Based on the cooperative principle, one can draw conversational implicatures
* At first glans B seems to violate the maxim of relevance by not directly answering A's question, but by looking at the utterly we can assume B is cooperative and wouldn't have said "he has a cold" unless it helped answer A's question

# Alignment
* Participants in a dialogue continuously align their mental representations
* Also unconsciously imitating each other at a deeper level (body language, way of speaking, speech rate, gestures, ...)


# Basic chatbot models
---
![[Pasted image 20231017153010.png | 500]]


# Rule-based models
* Maps conditions (surface patterns on user utterance) to responses
* Pattern-action rules
	* ![[Pasted image 20231017153101.png | 350]]
	* ![[Pasted image 20231017153115.png | 350]]


# Information Retrieval (IR) models
* $t$ is the utterence (words spoken/written)
* ![[Pasted image 20231017153232.png | 500]]
* Start with dialogue corpus
* Try to retrieve the most similar utterance in the corpus based on the corpus, then choose the next index
* How to determine which utterance is 'most similar' to the actual utterance?
	* Cosine similarity over some vectors 
	 * The vectors can be TF-IDF weighted words 
	 * Or utterance-level embeddings
* Example with TF-IDF:
	* ![[Pasted image 20231017153435.png | 500]]
	* ![[Pasted image 20231017153513.png | 500]]


# Dual encoders

* One encoder for the user input and one for a possible response
* Compute dot product (maybe with an activation function around) between user input and response vectors
* The two encoders often rely on a shared neural network, apart from a last transformation step that is specific for the context or response
* Dual encoders are trained with both positive and negative examples (good and bad answers)
* ![[Pasted image 20231017153847.png| 500]]



