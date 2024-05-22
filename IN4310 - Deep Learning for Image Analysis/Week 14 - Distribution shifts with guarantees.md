
* Distribution shifts in data
* Importance weighted [[Week 2 - Linear Models#Empirical risk minimization (ERM)|Empirical Risk Minimization]] for your data's test domain
	* Weight data points based on test domain
* Comparing distributions and discrepancy measures

# Distribution shifts
---

## Main challenges
### Dynamic environments:
* Perhaps the data is sometimes formatted differently?
* Many outliers in data
* For example:
	* Infection rates during a pandemic is different than normal
	* Automatic driving in snowy environments

### Domain adaptation:
* Training and test image distributions may be different in different datasets
	* ![[Pasted image 20240521135941.png|350]]
* One format on test and one on train set
	* ![[Pasted image 20240521135515.png|350]]

# Types of Distribution Shifts

* Formulas below uses the data ${(x_{i},y_{i})}$ and distribution $p$ #Maybe

## Covariate shift
_Distribution of the input features (covariates) changes between training/test data, but the conditional distribution of the output remains_
* Examples
	* Medical imaging: Various resolutions and equipment types
	* Agriculture: Diverse weather conditions and soil types
	* Robotics: Forest vs desert and sunny vs rainy scenarios
	* A model which predicts house prices is trained on large rural homes, with focus on the size of home/number of bedrooms. This might not work as well if used on houses in a rural area, with generally much smaller homes when the average distribution of input is different
* 
* $p^{tr}(x)\neq p^\text{(x)}$
* ![[Pasted image 20240521144215.png|350]]
* ![[Pasted image 20240521170242.png]]


## Label/target/class-prior shift
_Distribution of input features is the same, but distribution of labels is different_
* Can be described in change in class balance
* For example you trained on a lot of cats, but then you suddenly get a lot of dogs instead
* $p^{tr}(y)\neq p^\text{(y)}$

## Output noise shift/concept shift
_Target function which predicts x from x changes from training time_
*  $p^{tr}(y|x)\neq p^\text{(y|x)}$

## Class/conditional/concept shift
_Objects within a class might be different_
* For example if you train to classify European houses, but suddenly get a dataset with traditional asian style houses
* $p^{tr}(x|y)\neq p^\text{(x|y)}$

## Full distribution shift
_General case when distributions are different_
* $p^{tr}(x,y)\neq p^{tr}\text{(x,y)}$



# Weighing Empirical Risk Minimization for distribution
---

## Distributionally Robust Optimization (DRO)
_Optimize to minimize the risk over multiple distribution, not only the training distribution_

![[Pasted image 20240521171812.png]]
![[Pasted image 20240521175006.png]]
* $\hat{\mathbb{E}}$ is the empirical average
* Importance (density) ratio $r(x,y)=\dfrac{p^{te}(x,y)}{p^{tr}(x,y)}$
* Importance weighting is consistent
* Learned function converges in probability to optimal test error minimizer

### Importance Weighted ERM (IWERM)

* Convergence in probability is established using the law of large numbers
* ![[Pasted image 20240521175509.png|400]]
