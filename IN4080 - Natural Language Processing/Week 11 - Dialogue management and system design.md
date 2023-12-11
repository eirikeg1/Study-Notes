
# Spoken dialogue systems/-management

## Challenges

* Uncertainties, ASR errors etc.
* Speech communications more than just words (intonation, emotions in voice, etc.)
* Turn taking

## Speech production

* Variations in air pressure
* Produced with 3 components in body
	* Air supply (lungs)
	* Sound source (Setting air in motion, by vibrating)
	* 3 filters (pharynx, oral tract, nasal tract)
* Some languages also relies on other sounds not made by vibrations, for example click languages

## Speech perception

### Important measures

* Fundamental Frequency $F_0$
	* Lowest frequency of the sound wave, corresponding to the speed of vibration of the vocal folds
* Intensity
	* Signal power normalised to the human auditory threshold measured in dB
	* ![[Pasted image 20231031142729.png | 500]]

### Speech recognition task

* Uses overlapping sequences
* Difficult because there are many sources of variation: speaker voice and style, accents, ambient noise
* ![[Pasted image 20231031142816.png | 650]]


## Preprocessing

* Most sounds cannot be distinguished from raw waveform
* Better: convert the signal to a representation of the signal's component frequencies
	* Based on Fourier's transform
* ![[Pasted image 20231031143442.png | 500]]

## Neural Automatic Speech Recognition (ASR)

* Best performing ASR are deep, end to end neural networks
* For example a relatively simple model is Googles on device ASR
	* Encoder maps audio signal $x_t$ to hidden representations with stacked LSTMs
	* Prediction network is a language model
	* Model merges the two hidden representations and predicts outputs character-by-character
	* ![[Pasted image 20231031143546.png | 500]]
* 

## Evaluation

* **Word Error Rate**
	* Measures how much the utterance hypothesis h differs from *The gold standard* transcription $t^*$
	* Minimum edit distance between h and t*, counting the number of word substitutions, insertions and deletions
	* ![[Pasted image 20231031144910.png | 500]]
	* ![[Pasted image 20231031144938.png | 500]]


### Disfluencies

* Speakers construct utterances as they go, incrementally
	* This is noticed in speech stream when you talk
* Pauses, fillers (*"um"*, *"liksom"*)
* Repetitions (*"The the ball"*)
* Corrections (*"the ball err mug"*)
* Repairs (*"The bu/ ball"*)


# Design of dialogue systems
---

## Decision making

* What and when should the system decide to say or do something
* Decision making under uncertainty, since the communication channel is noisy
* Actions can be both linguistic and non-linguistic
* The same holds for observations (visual input, external events, etc.)
## Typical pipeline

![[Pasted image 20231031145804.png | 500]]


![[Pasted image 20231031145825.png | 500]]


# Handcrafted approaches

## Interaction style
* Rigid, repetitive structure of the interaction 
* Irritating confirmations & acknowledgements 
* No user or context adaptivity
* 
## Finite-state automata

* Flow chart representing input to actions
* Transitions can relate to other signals than user inputs (for example external events like weather)
	* Can also be complex conditions
* ![[Pasted image 20231031150126.png | 500]]
* ![[Pasted image 20231031150245.png | 500]]

### Pros and cons

![[Pasted image 20231031151630.png | 500]]

## Frame-based managers

* Interaction flow can be made slightly more flexible in the frame based systems
* State is represented as a frame with slots to be filled out by users answer
* If user provides additional information (user says time as well):
	* System: What is your departure? 
	* User: I want to leave from Oslo before 9:00 AM»
* System tries to fill as many slots from answer, asks questions until all required slots are filled
* ![[Pasted image 20231031151747.png | 500]]



# Data Driven approaches

## Struggles
* Difficuly to predict user behaviour in advance
* Ignore all the uncertainties appearing through the dialogue (ASR errors, ambiguites, etc)
* Unable to learn or adapt to the users or the environment (leading to rigid/repetitive behaviour)
* Limited to one goal. But real interactions are trade-offs between various competing objectives

## Solution
* Solution: perform automatic optimisation of the «dialogue policies» from experience:
	* Often by reinforcement learning
	* Sometimes starts with supervised learning, but adapted by reinforcement learning
* Dialogue manager starts with 'dumb' dialogue poicy but iteracts with and receives feedback from users
* Usually encoded with a reward function (is it good or bad?)
* ![[Pasted image 20231031152824.png | 500]]

## Markov Decision Processes

* Extension of **Markov chain**, but the agents selects an action at each state
* **MDP** is as a tuple $<S,A,T,R>$ where: #toExpand 
	* $S$ is the state space (possible states in domain)
	* $A$ is the action space (possible actions for the agent)
	* $T$ is transition function
	* $R$ is the reward function
* Agent seeks to maximise its *expected cumulative reward* $Q(s,a)$
	* Must try to predict future inputs/rewards
	* Rewards accumulate over time
* How much worth is a reward expected at time (t+i) compared to one reward received right now?
	* Calculated by discount factor $y$ 
	* Related to delayed gratification in psychology
* ![[Pasted image 20231031152937.png | 500]]
* ![[Pasted image 20231031153010.png | 500]]

# Reinforcement learning

* Can help us learn Q values through interaction
* Works by refining estimates of Q values
	* Agent acts in environment and observes states and rewards
	* Repeated until convergence
* In dialogue systems: policy learning can be done either in simulation or with real users

### Expected cumulative rewards

#### Bellman equation

* Expected cumulative reward $Q$ in a recursive fashion
* Estimates the Q values based on out estimation of the Q-values, can be uI sed to iteratively refine estimates until conversion
* ![[Pasted image 20231031153631.png | 500]]
* 

#### MDP policy #toExpand 

* Dialogue policy tells us which action to execute in each state
* Dialogue policy is a mapping $\pi:S->A$ from states to action
* An optimal dialogue policy $\pi^*$ is a policy which always outputs the action yielding the maximum expected cumulative reward
* ![[Pasted image 20231031154431.png | 500]]

## Pipeline architectures #toExpand 

## How to collect data?

* *Chicken and egg* problem:
	* Need data to train data-driven models
	* But to collect data, we need a system that can itnerct with users
* *Wizard of Oz*
	* Replace the system with a human operator (without the users being aware of it)
	* Gives insight for quality

## Evaluation

* **ASR: Word Error Rate**
* **NLU: precision, recall, F-score**
* **TTS: Evaluation by human listeners on sound intelligibility and quality**
* What about end-to-end?
	* User satisfaction? Can be expensive and time consuming
		* ![[Pasted image 20231031155656.png | 500]]
	* Rely on metrics that can be extracted from interaction logs, and are known to correlate with user satisfaction
		* ![[Pasted image 20231031155807.png | 500]]
* **BLEU** has been used to compare, but is not very good with user satisfaction
* Alternative metrics exist, like **ADEM**






* 