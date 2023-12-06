 # Week 13
#toExpand 


# Misuse of AI
---
## Dual use
_tech can be used for peaceful&military

* recon
* weapons

## Surveillance

* Data trails
* Building up detailed profiles


# Privacy & trust
---

## Privacy

* **GDPR**
* Personal data cant be processed, stored or shared without consent
* There are some exceptions in a few of the rules, for health personell for example

### Anonymisation

* Direct identifiers (personal ID) must be removed
* Quasi identifiers (alone not enough to identify, but combined they can) are more tricky
* Sensitive attributes: another factor to consider how sensitive the attribute is

#### Practically impossible without deleting actual data
* Anonymised data can often be linked back to original data without destroying most of it
* **NLP** can be employed to detect and edit out personal identifiers
	* Will only minimize, you don't know if it is anonymised

## Trust

### Explainability

* Deep learning models are black boxes
* This opacity is problematic
* **GDPR** mandates *right to explanation*

* Very active research topic in ML/NLP (explainability)
* Current methods work by converting learned neural net to simpler model
	* For example **LIME**
		* Local approximation with a linear model
		* Specify a linear model for each point, and look at most important features
		* Gives us the weight of each feature in the decision
		* ![[Pasted image 20231121150942.png | 350]]
		* ![[Pasted image 20231121151820.png | 350]]