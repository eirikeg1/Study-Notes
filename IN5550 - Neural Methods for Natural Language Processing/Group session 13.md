
# Logging
---

* Libraries: 
	* historically: `tensorboard`
	* `Weights $ Biases$`
	* `Neptune`
	* `Comet`
	* `MLFlow`


## How
```Python
import wandb

wandb.init(
    name="Cosine LR",
    entity="Your username goes here",  # <<======
    project="IN5550_session_04"
)

# Initialization code
...

for epoch in dataloader:
	# Train code here
	...
	
	wandb.log({
            "epoch": epoch,
            "grad_norm": grad_norm.item(),
            "learning_rate": optimizer.param_groups[0]['lr'],
            "train/loss": loss.item(),
            "train/accuracy": accuracy(predictions, classes).item()
        })
    
```



# Reduce memory
---

## Checkpointing



