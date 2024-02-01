
## Tensors
* Tensor = n-d arrays
* All tensors must be on same device

## Broadcasting
_Functionality which allows one to perform mathematical operations even when tensor shapes are mismatched_

* Multiplying $[1, 2, 3, 4,]$ times $[[1], [2]]$ turns to $(1,4)$ times $(2,1)$
* Corresponding shape entries must be equal, or one of them 1
* The shape of tensor with fewer dimensions can be appended by 1's from the left
	```python
	a = torch.ones((1,7))
	b = torch.ones((5,2,3,7))

	c = a + b # Still (5,2,3,7), as a shape is changed to (1,1,1,7)
	```

## Defining dataset

* PyTorch datasets require ```__getitem__``` and ```__len__```
* In order to create a dataset make a class which inherits from PyTorch's ```torch.utils.data.Dataloader``` class
* Dataloader class allows shuffling, parallelizing and loading across multiple workers

# Operations
---

### Running on CPU

```Python
t = torch.ones(5)
b = a.detach().cpu().numpy()

```

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


## Tensor operations
_Tensor variable is noted with 't'_

### Creating tensors

```Python
t = torch.arange(5)
torch.ones(5, 2, 3)
torch.Tensor()
torch.clone(t) # Clones tensor 't', points to same memory
torch.copy(t)
torch.deepcopy(t)
torch.randn(3, 5, 6)
```


### Shape

```Python
t.reshape(3, 4)
t.reshape(3, -1)   # -1 is a wildcard, automatically fitted to data
t.view(3, 4)       # Create copy of tensor to (3, 4)
t.T                # Transpose tensor

torch.transpose(t) # Transpose tensor
torch.permute(t, (1, 2, 0)) # Changes the indexes of elements
```


### Multiplication
#toExpand

```Python
torch.dot(a,b) # Dot product between tensors 'a' and 'b
torch.mm(a,b)  # Matrix multiply 'a' and 'b'
torch.bmm(a,b) # Batch matrix multiply
torch.einsum('bij,bjk->bik', A, B)
```


$\phi(x_i,t_j)=e^{-\dfrac{||X[i,:]-T[j,:]||^2}{\sigma}}$
