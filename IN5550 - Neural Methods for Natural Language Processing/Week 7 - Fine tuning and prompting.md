

![[Pasted image 20240328215923.png|250]]

# Downstream fine-tuning
---

* Usually transfer learning from self-supervised task to supervised task
* But in general fine tuning refers to any kind of training that adapts/specializes a pre-trained model
* First, train general model and then specialize on a downstream task
* Language model can be either **Frozen** or **further trained**

## Fine-tuning of BERT

* Almost always overparameterized for the supervised data
* Be careful with overfitting
* **BERT** is used to do **MLM**, not our supervised task
* [[Week 2 - Practicalities and hyper-parameters#Regularization|Regularization]] is important
	* Large weight decay (0.1 by default), early stopping (usually enough to train for just 2-8 epochs) and dropout
* **Learning rate schedule** is crucial
	* Peak LR should be small (around 3e-5 for **AdamW**), and should have warm-up

![[Pasted image 20240328220218.png|350]]


## Fine-tuning GPT

* Can be done similarly to **BERT**, but mask is always at the end
* Can also be done more similarly to **T5**
* Is autoregressive

![[Pasted image 20240328220836.png|350]]


## Fine-tuning T5
_Text-to-text transfer transformer_

* Does not need any classifier, reformulate classification tasks as sequence-to-sequence tasks



# Prompt-Based Learning
---

## Supervised learning

* We don't always have a big enough dataset to fine-tune the model, we can instead use a prompt template that can transform any input-output pair into natural text
* 
 
### Filled prompt
_Contains the input x and answer y_
![[Pasted image 20240328224625.png|350]]


### Cloze prompts
_Generate the masked token in the prompt_
* Generate the output directly
![[Pasted image 20240328225117.png|350]]

### Prefix prompts
_Give a prefix sentence with instructions, model generates the rest of the sentence/s_
* Used for Casual Language Models


### Few-shot prompts
_Give 'a few' annotated gold examples in the start of the prompt_

* Can be multiple examples, fex. 3-shot or 5-shot prompts
![[Pasted image 20240328235359.png|350]]

# Instruction Fine-Tuning
---
_Fine-tune a general LM to act as an obedient expert assistant that factually answers our questions_

* Improves the performance of language models, **FLAN** outperforms few-shot **GPT-3** with zero shot!
* Generalizes and outperforms 'pure' language models

## Alignment
_Make the LM play the role you want_
* LMs are pre-trained on enormous amounts of texts, so they can imitate all kinds of characters and domains (article by a nuclear physicist, blogpost by a conspiracy theorist, or a mean comment by an internet troll)
* Goal is to align with user intent

## InstructGPT
_Method used to fine-tune for example GPT-3 to be better at conversational instructions_

* Instead of fine-tuning on 'artificial' NLP datasets, like used by **FLAN** models, it is fine-tuned on more human problems
* 
* ![[Pasted image 20240329001140.png|400]]

### Steps

1. Manually create a dataset with prompts and gold answers
2. Then we instruction fine-tune a LM on this data
3. Then we take this model, generate a bunch of answers to every prompt from a new dataset and manually rank these answers
4. Then we train a special reward model that assigns a score for every pair of prompt and answer
5. Then, finally, we use the reward model to fine-tune a language model with **proximal policy optimization**

![[Pasted image 20240329001538.png|350]]


## Proximal Policy Optimization (PPO)
_Deep reinforcement learning algorithm to optimize the behavior of an agent according to a reward function_

* In **InstructGPT**, the environment is a human (who has a question and rates the answer, the agent is the language model and its action generates a new token)
* The problem with **Deep Reinforcement Learning** is that when the agent performs actions the consequences in the environment are not differentiable, so you can't just maximize the reward
	* We use an **actor-critic** algorithm, where the actor model performs actions and the critic is a world model that simulates the environment and approximates the reward function
	* Critic is a neural network (which is differentiable), so we can teach the actor to maximize the critics reward
	* **PPO** is an actor-critic algorithm with some minor improvements
* Basic idea (reality is more complicated and involves a lot of ad-hoc hyper-parameters):
	* ![[Pasted image 20240329002528.png|350]]