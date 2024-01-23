
## Tensors
* Tensor = n-d arrays
* All tensors must be on same device


## Broadcasting
---
_Functionality which allows one to perform mathematical operations even when tensor shapes are mismatched_

* Multiplying $[1, 2, 3, 4,]$ times $[[1], [2]]$ turns to $(1,4)$ times $(2,1)$
* Corresponding shape entries must be equal, or one of them 1
* The shape of tensor with fewer dimensions can be appended by 1's from the left

## Defining dataset

* PyTorch datasets require ```__getitem__``` and ```__len__```
* In order to create a dataset make a class which inherits from PyTorch's ```torch.utils.data.Dataloader``` class
* Dataloader class allows shuffling, parallelizing and loading across multiple workers

## Operations
---

### Matrix multiplication

* ```torch.mm(a,b)``` is without broadcasting
* ```torch.matmul(a,b)``` is with broadcasting

### Autograd
_Automatically calculate gradients of computational graph_

* PyTorch keeps track of gradients of the computational graph when executing differentiable operations
* ```loss.backwards()``` calculated all gradients backwards
* When not training you do not want to calculate gradients, then you should use the ```no_grad``` context manager
	* ```no_grad()``` makes sure PyTorch does not track any gradients
	* ```with torch.no_grad()
			# Code```
### Optimizers
_Built-in optimizers that can be used for gradient based optimizations_

* When doing a forward pass call ```optimizer.zero_grad()```





