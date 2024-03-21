
## Running the code
---

The code can be run with:

```Python
python3 Assingment1.py
```

This will run all the three tasks, including the grid search in part 1. Running everything can be very time consuming, therefore I have added som optional parameters:

```
--task <int> : choose which task to run
--skip-grid-search: Can be used with task 1, uses the stored model instead of training a new one.
```

Because running task 3 requires task 2, task 2 will also run if `--task 3` is used.

## Task 1
---
### Data split
The two classes I have to manage my data is in the `Data.py` file. The class `DataSplit` reads the files, splits it and asserts they are disjointed. The class `ImageDataSet` takes a list of images and corresponding labels, as provided by `DataSplit` and implements the PyTorch Dataset interface.

### Model
For this task I chose to use `ResNet18` as the model and `CrossEntropyLoss` for the loss function. I made class `ResNet` which contains all of the code done for the model. This includes al training, evaluation and plotting. The saved model is found in the `models` folder.

### Hyper-parameters
The hyper parameters I chose to explore was optimizer and if to augment the image set or not. The **augmentation** is a 50% chance to randomly flip and/or rotate the image. For both examples it was better. The two optimizers I tested was PyTorches `SGD` and `AdamW`. `AdamW` outperformed `SGD` in both runs.

### Plots
Plots of loss can be found in the `plots` folder. The loss curve was as expected: the train loss did steadily decrease. The validation loss was a bit more chaotic, it went down first, but after 3 epochs it started to go up. This is probably because of overfitting to the training data.

## Task 2
---
The output is stored in the file: Task2 out. I chose feature maps for layers spread throughout the model on layers: 2, 30, 55, 80, 110. The respective percentages was: 70.48%, 32.74%, 23.48%, 33.35%, 47.65%. As expected it stats with a high percentage


## Task 3
---
I ran into some shaping problems right before the delivery, however I believe I am very close