
## Good images
Most of the images were good. The model seems to predict the correct spots correctly, maybe with slightly different jaggedness of the border. But Most of the shapes seems correct. All the 5 images can be found in the folder `good_images`
![[Pasted image 20240424171002.png]]
![[Pasted image 20240424170945.png]]
![[Pasted image 20240424171017.png]]
![[Pasted image 20240424171030.png]]
![[Pasted image 20240424171041.png]]

## Bad images
All of the images I checked seemed fine. The only exception is in the few images where the label is almost empty, then the prediction tends to classify a few spots which should not be classified. In other words, in empty images it can have a slight problem with TrueFalse predictions. But since this is a rare case, and it never predicts a lot it does not seem like a big problem. The two images can be found in the folder `bad_images`

![[Pasted image 20240424170914.png]]
![[Pasted image 20240424171117.png]]

## Model performance
The final model got a Dice score of **0.8553** on the validation set and **0.7948** on the test set. I ran it for **30 epochs**, with a **learning rate of 8e-4**. The original learning rate did not seem to converge, as it fluctuated a lot, especially around epoch 10-20. But when I lowered it is went down in a much more stable fashion.
 
### BCE loss

![[Pasted image 20240424171335.png]]

### Dice loss

![[Pasted image 20240424171352.png]]

![[Pasted image 20240424165750.png]]

![[Pasted image 20240424165731.png|300]]


