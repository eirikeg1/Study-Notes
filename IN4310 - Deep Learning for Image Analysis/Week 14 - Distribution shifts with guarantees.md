
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

## Types of Distribution Shifts

* Formulas below uses the data ${(x_{i},y_{i})}$ and distribution $p$ #Maybe

### Covariate shift
_Marginal training and test distributions are different_
* $p^{tr}(x)\neq p^\text{(x)}$
* 

### Label/target/class-prior shift
_The actual distribution is similar, but the classes are different_ #Maybe
* For example you trained on a lot of cats, but then you suddenly get a lot of dogs instead
* $p^{tr}(y)\neq p^\text{(y)}$

### Output noise shift/concept shift
_Target function which predicts x from x changes from training time_
*  $p^{tr}(y|x)\neq p^\text{(y|x)}$

### Class/conditional/concept shift
_Objects within a class might be different_
* For example if you train to classify European houses, but suddenly get a dataset with traditional asian style houses
* $p^{tr}(x|y)\neq p^\text{(x|y)}$

### Full distribution shift
_General case when distributions are different_
* $p^{tr}(x,y)\neq p^{tr}\text{(x,y)}$