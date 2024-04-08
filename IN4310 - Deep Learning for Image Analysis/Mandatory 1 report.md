
## Attempt 2 changes
---

Here are the changes I made for the second attempt. 
* I added the method `ResNetModel.image_class_probabilities()`, which returns a dictionary where the keys is the name of the images, while the values is the logit list
* I created the file `save_10_best_and_worst.py`, which loads in the model, uses the class explained above to calculate the logits and then saves the best/worst images for each class in the folder `best_worst_images`
* Updated the `Assignment3` and `ResNetModel.PCA()` to correctly calculate the `PCA` graphs. The method calculates the values and saves a graph in the `pca` folder.


### PCA
The graphs can be found in the `pca` folder. For some reason both the fine tuned version and the non-fine tuned seems to cluster kind of similarly. However I notice that the not-fine-tuned version does not actually predict all the classes, while the fine tuned does.

Even though all the classes seems to be centered approximately around origo, I notice that each class seems to have a different average distance between the points in the  fine-tuned model, while the average distance is more similar between each datapoint for each class in the not fine-tuned model. This makes me think that there is actually a difference in the vectorspace, however that the `PCA` might have picked up on slightly wrong dimensions (as the expected output is different centroids).

### Best/worst images results

It is not completely fair to compare the softmax of different images across multiple predictions, as softmax values are computed relative to each other for each image. Therefore a high score does not show exactly how _good_ an image is, rather which classes out of the relevant ones fit the most, compared to each other. In practice images which does not fit any of the classes, but one more then the others might get a very high score for that class, even though the model is not quite sure. This is important to note for the analysis.

The results are stored in the `best_worst_images` folder. Because it was a simple for loop, I chose to just save it for all the classes. 

The model struggled a lot with the `street` class and gave high probabilities to a lot off `sea` class images. I think this makes sense as if you look at the high probability images of `sea` there are a lot of seas where the actual ocean takes a similar shape as the street in the `street` images. The `street_best_1.png` is a `building` image from up front. This is probably because a lot of street images has buildings depicted from in front. The image points upwards with buildings on each side, so it is probably taken from a street, perhaps the un-fine-tuned model would predict this image differently

Both the high probability `sea` images and `street` images also had a tendency to have houses with lights around them. This might be a detail the model can have picked up on. If I had trained the model for more epochs the model might perhaps have picked up on some more details which might make the model better at picking out these details.

The `forest` class seemed to categorize `glacier` pictures highly. My guess is, again, that it could be improved by training for more epochs. This is because the `forest` and `glacier` tags are both `nature` themed (not in the dataset but just generally) trained on completely different labels. Therefore it might give these types of images similar scores as it still looks at them as similar. However fine-tuning more might make it cluster them more into our classes.

The `building` and `mountain` classes seems to be the best classes by looking at the pictures. The `building` classifies a forest image as the 10th highest. Perhaps it is because a lot of buildings can have plants beside them or within their courtyards? The fact that all the top 10 `mountain` pictures are classified correctly makes sense as mountains have very characteristic shapes.


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