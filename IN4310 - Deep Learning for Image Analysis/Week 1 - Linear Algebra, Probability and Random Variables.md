

# Linear Algebra #toExpand
---

* Eigenvalues/eigenvectors
* Matrix calculus: Gradient
* Hessian matrix


# Probability
---

* **Sample space** $\Omega$ the set of all sample points for a given experiment
* **Events** are subsets of the sample space, $A^c$ complement of an event. $A$ is the set of points in $\Omega$ but not $A$
## Axioms for events
* $\Omega$ is an event
* For every sequence of events $A_{1}A_{2},\dots ,A_n$ is an event
* 

## The 2 axioms of probability

* A **Probability rule** $Pr$ is a function mapping each event to a real number so that $Pr(\Omega) = 1$ 
1. For every event $A$: $Pr(A) \ge 0$
2. For **disjoint events** $A_{1},A_2,...,A_n$ where these events cannot happen simultaneously (no event shares outcome with another), the probability that any of these happen is equal to the sum of their individual probabilities

## Properties of probability rule $Pr$


## Bayes Rule


## Random Variable and Distribution function

### Discrete random variable
* Takes on a countable number of distinct values

### Continuous random variable
* Takes an uncountable number of values
* For example the amount of time it takes for a computer to process a certain height

## Probability density/mass


## Markov's Inequality
_Applies an upper bound for the probability that a non-negative random variable is greater then or equal to a certain positive value_

* Given a non-negative random variable $X$ and a positive constant $a$
* $P$ denotes the probability
* $E(X)$ is the expected value of $X$ 
* $a > 0$.
* Formula: $P(X \geq a) \leq \frac{E(X)}{a}$

## Hoeffding's Theorem

* Assume $( X_1, X_2, \ldots, X_n )$ are independent random variables, which are bounded such that $( a_i \leq X_i \leq b_i )$ for each $( i = 1, 2, \ldots, n )$
* Let $\bar{X} = \frac{1}{n} \sum_{i=1}^n X_i$ be the sample average $\bar{X}$
* then for every $t>0$, $P\left( |\bar{X} - E[\bar{X}]| \geq t \right) \leq 2 \exp \left( -\dfrac{2n^2 t^2}{\sum_{i=1}^n (b_i - a_i)^2} \right)$



