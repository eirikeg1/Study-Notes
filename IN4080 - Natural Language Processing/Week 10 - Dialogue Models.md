
# NLU-based chatbots
---

* If you don't have a good corpus
* NLU as a **classification tasks**
* For a set of (predefined) possible intents
	* For example for voice assistant: *Read out the weather?*
* Response selection generally handcrafted


## Intent recognition

* Map user utterance to its most likely intent
* *Input*: sequence, *Output*: intent
* Often used with LLM classification heads (softmax at end)
* Need to get training data to learn this classification model
	* User utterances + corresponding intents
* CLS token represents the class for all the tokens
* ![[Pasted image 20231024143219.png | 600]]
* Standard approach:
	* Take pre trained neural language model (NorBERT for Norwegian)
	* fine tune it for this specific classification task


## Slot filling

* Sometimes we need to detect specific entities or slots, such as mentions of places or times
* ![[Pasted image 20231024143321.png | 500]]
* Slots are domain specific
* Can be framed as a *sequence labelling task* 
* Intent classifier and slot filler can be fine tuned on same model
* Token-level classification task (output classes: BIO-prefixed categories)
* ![[Pasted image 20231024143359.png | 500]]


## Response selection

* In commercial systems, system responses are typically written by hand
	* Maybe in templated form: *{place} is open from {start-time} to {end-time}*
	* Data-driven generation methods also exists


## To little data?

#### 1.  Use transfer learning to exploit models on related domains
* For example use a pre-trained language model and then fine tune
* Could also be trained on a similar domain if there are a lot of similarities
* ![[Pasted image 20231024144413.png | 500]]

#### 2. Use data augmentation

* Generate new labelled utterances from existing ones, using small changes without changing meaning
* Maybe translate to different languages (Maybe translate back to get a slightly different formulation in same language)
* Generate new formulations with for example chatGPT
* Gives a bigger training set with correct information
* ![[Pasted image 20231024144903.png | 500]]

#### 3. Label more data
* Manually or using weak supervision techniques
* Weak supervision techniques can automatically label data

#### In-context learning to provide examples as part of the prompt
#toExpand 
* Change prompt for better results
* For example automatically add examples to the prompt or interpret/reformulate the prompt



# Generative models
---

* Seq2seq models generate response token by token
	* Can generate new responses never observed
* Two steps:
	1. First encode input with neural model
	2. Decode the output token by token


## Types
#### Encoder-decoder models
* Self-attention + cross attention
* Cross attention between encoder and decoder
* Popular for masks like MT and summarization
* ![[Pasted image 20231024152038.png | 500]]

#### Decoder-only models
* GPT models
* Same model which encodes and decodes, using attention for each word
* Has become dominant

Overview of types:
![[Pasted image 20231024151701.png | 350]]



# Decoding

* Can be done greedily by always choosing the most likely
	* Can give boring answers like: *I don't know*, *Ask wikipedia* 
	* Does not explore partial probabilities (first word very likely but the rest are bad)

#### Beam search #toExpand 
* Keep at each time a set of $k$ partial hypothesis
* Expand these until $<eos>$
* For example if dog is 
* ![[Pasted image 20231024153802.png | 500]]
#### Sampling
* Temperature controls the 'creativity' of the response
* Lower temperature = *sharper* distribution (increases likelihood of high probability words and decrease the likelihood of low probability words)
* ![[Pasted image 20231024154325.png | 500]] #updateImage

#### Top-K sampling
* Select the $k$ tokens with the highest probability, redistribute the probability mass among them, and sample from that distribution


# Fine tuning methods
---
## Instruction fine tuning

* Systems like ChatGPT are not raw LLMs, they are fine-tuned to follow instructions and/or engage in a dialoge with the user
* Many open-source LLMs have downloadable models that are instruction fine tuned
* ![[Pasted image 20231024154722.png | 500]]

## Domain adaptation

#### **In-context learning**
* Adding <input, response> pairs as part of the prompt
* Can only include a small number of examples because of context window
* Can be slow, as e longer context must be encoded
* Ok for prototype, but limited domain adaptation

#### Parameter efficient fine tuning (PERT)
* Don't change all parameters/weights
* Change or add new parameters
* Add adapter layers (small neural network layers which are trained individually)
* **LoRa**: small number of learned parameters (millions) on top of the original frozen ones
* Can be difficult and expensive to update all parameters, but this is not always needed

#### Prompt tuning
* Search for the best possible prompt, keeping model frozen
* Can be a soft prompt (prefixed vectors instead of actual words)

# Challenges
---
## Factuality
* Not trained for facts, but plausible words
* Can still hallucinate with a *perfect* dataset

## Controll
* LLMs are black boxes
* Can steer the model by prompting with specific instructions, fine tuning or reinforcement learning
	* But still unpredictable
	* Side problem: How to delete information from a language model? (cf. GDPR’s right to be forgotten)

## Multimodality
* Add visual or other capabilities

## Retrieval-augmented models

* Retrieves data from a corpus, and then generating
* Uses a **Retriever** and a **Generator**
* Knowledge base can be easily inspected and updated (add/remove docs)
* Can help reduce hallucinations
* ![[Pasted image 20231024160038.png | 500]]

