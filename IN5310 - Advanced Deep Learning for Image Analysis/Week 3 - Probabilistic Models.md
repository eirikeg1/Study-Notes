_Probabilistic models rely on a framework where we model the distributions of the data and other hidden variables to exploit their relations to perform our tasks._


# Variational Inference
---
_Approximate estimation, solves a problem by defining a tractable family of distribution $\mathbb{Q}$ most similar to $\mathbb{P}$._
* Unlike Monte-Carlo based approaches, variational approaches are not designed to find the true probability distribution of the data, but provides defined convergence criteria, algorithms amenable to parallelization, and integration with gradient based approaches
* Effective for deep learning

## Mean Field Inference
* Decide on a probability distribution with a probability density function (pdf) q and assume the dimensions can be factored as $\displaystyle{q(x)=\prod_{i\leq dim(x)}q(x_i)}$
* First step in **Variational Inference** is to decide on a suitable family


## Kullback-Lieber (KL) Divergence
_Way to measure similarity between different probability distributions_
![[Pasted image 20240910112514.png|500]]

* Quantifies how one probability distribution diverges from a second, expected probability distribution.
* It is not symmetric, therefore not a formal metric distance, but a member of class of fucntions known as _f-divergences_


# Variational Autoencoders

## Autoencoder
* Maps into to lower dimentional representation
* Can be used with an autodecoder to usually map back (or to similar)

## Evidence Lower Bound
