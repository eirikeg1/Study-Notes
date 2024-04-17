

# Question Answering
---
* Traditional task within NLP

## Question Answering as a task
_A question answering system is a computer program that can answer questions formulated in natural language_

* Specific formulation has historically varied a lot, as almost anything can be reformulated into question answer pair
* Questions can be separated into **Information-seeking** or **Probing questions**
* 
### Information-seeking
_You want to learn something to don't already know_
* Google searches, StackOverflow questions, etc
* Typically assumes there is no additional context
* Open-ended answers (can be running text, lists, images, whatever)

### Probing questions
_When you want to test a machine on something you already know_
* Used to evaluate computer programs
* Typically assumes some context, e.g. a provided passage
* Also referred to as **machine reading comprehension**
* Often formulated in a multiple-choice format


## Visual Question Answering
_Questions relating to visual reasoning, e.g. attribute identification, counting, comparison, spatial relationships and logical operations_

* Hard to get right
* ![[Pasted image 20240414225140.png|400]]


## Question formats
_Different ways of asking/answering _

### Extractive
_Answer with an extract from the context_

### Multiple-choice
_Choose one of a set of given options_
* Choose a, b or c

### Categorical
_Choose a category_
* For example True or False

### Freeform
_Generate an output_
* For example an LLM
* More difficult than the others


## Domains (scope)

### Open-domain
_The questions target a wide range of sources, and are not limited to one specific domain_

### Closed-domain
_The questions targets only one domain e.g. medicine_

### Open-book
_The model has access to information external to the question and any provided context e.g. the whole of wikipedia_

### Closed-book
_The model does not have access to anything outside the question and has to rely solely on the provided information and any knowledge already stored in the system (e.g. weights)


# Different Approaches for Question Answering
---
## Encoder only BERT
_Was efficient for question answering_

* Question and  context are sent into the model, separated by a **[CLS]** token
* Good for answering short questions, like *What is the capital of France?* or multiple choice
* ![[Pasted image 20240414224902.png|500]]


## Decoder only models (LLMs)
* The two core problems for LLMs and question answering is that, the models store knowledge implicitly in a huge parameter space and the weights are expensive to update

### Implicit storage
_The weights are a black box, so we don't really know what to change to update specific parts of models knowledge base_
* You have to train the whole model to change small parts
* Can change other things you do not want to change

### Weights are expensive to update
* General facts, like for example capitals are updated very rarely, as the information is mostly static
* More specific things, particularly when in a smaller more specific domain, can change constantly

## Retrieval Augmented Models
_Can be used to leverage information from external knowledge, used to mitigate the two core problems of LLMs_