
# TODO
* Test dribbling detection algorithm:
	* Test on smaller subset where you know videos are mislabeled or misclassified
	* With all entities converted to players (maybe except for "other")
	* Without team differentiation
	* Compare longer/shorter videos

# Player object detection
---
## Results
### Initial experiments
* Default model
* High quality bounding box predictions
* Did not manage to detect the balls
* Low quality object class on external datasets
	* Goalkeeper, referee, player, other is often problematic
		* ![[Pasted image 20250128180418.png]]
	* Referee overfits on yellow shirt and black shorts
		* ![[Pasted image 20250128173945.png]]

### Second iteration
* YOLO11m finetuned on soccernet gs data (640px images)
* Ball and player in one model
* Ball is now sometimes detected
* Around the same speed
* Lower confidence allows for ball to be detected more often, but also results in multiple boxes on some players (especially blurred players)
### Third iteration
* YOLO11s finetuned on soccernet gs
* Image size is now increased to 1080px
* Faster training, much faster convergence
* Greatly improves on both MaP scores on the validation set
* Ball and player in one model
* Better at detecting the balls, but low confidence is still needed for consistent enough results
* Confidence of around 0.3 is very consistent with ball, but occationally doubles bounding boxes over blurred players, especially in low resolution footage
* ![[Pasted image 20250205202550.png]]
* The ghost frames are then interpolated over multiple frames, both bounding boxes and 2d coordinates
	* ![[Pasted image 20250205202251.png]]
* **Lowering the iou threshold** removes the ghost frames, but since the player coming from behind is tracked to the right of the frame both before and after merging, his bounding box is interpolated behind the bounding box
	* Notice how the defending bounding box is just within the inner rad, triggering a potential drible event if the possession holder retains the ball
	* ![[Pasted image 20250205203443.png]]
* After these frames a new player id is created in front, then the player gets back its original id behind
	* ![[Pasted image 20250205203708.png]]
	  ![[Pasted image 20250205203716.png]]

## YOLO model training
* Gradually improving
* When training on player and ball:
* **For future research:**
	* Fine tune model on different data
	* Specialized model for predicting ball


### After about 25 epochs
* For yolo11m on ball/player 640px
![[Pasted image 20250203224426.png||400]]
### Class Distribution (Top-Left Bar Chart)
- Observation:
	- The dataset contains significantly more player detections than ball detections.
	- Players: ~1.5 million instances.
	- Ball: ~100,000 instances.
- Implications:
	- This imbalance could affect the model’s ability to detect the ball reliably, as it may be biased towards detecting players.
	- If ball detection is critical, you might need to apply **oversampling** (augment ball images) or **class-weighted loss** during training.
### Bounding Box Center Distribution (Bottom-Left Heatmap)
- Observation:
    - The heatmap shows where objects (players and balls) are most frequently detected in the normalized image space (0-1 scale).
    - The densest region (darkest area) is around **y ≈ 0.5 - 0.6 and x ≈ 0.4 - 0.6**.
    - This suggests that most objects are **centered around the middle of the image**.
- Implications:
    - Can be bad for different camera angles where players are more spread out
    - If this dataset is for football matches, it makes sense as the center of the field is where most events happen.
    - However, if you want robust performance in different field areas, consider ensuring **even distribution** of labels across the image.
    - If the dataset primarily focuses on central players, the model might struggle with detections near the edges.

### Bounding Box Width vs. Height Distribution (Bottom-Right Heat map)
- Observation:
    - Most bounding boxes are clustered in a small width-height range.
    - Players seem to have a more consistent size, while the ball appears in a tighter range of small sizes.
    - Bounding box widths are mostly between **0.01 and 0.05**, and heights are between **0.05 and 0.15**.
- Implications:
    - If the dataset lacks larger or smaller instances of objects (e.g., players near the camera vs. far away), the model may struggle with scale variation.
    - Using **multi-scale training** (randomly resizing images) or applying **scale-aware augmentations** might improve robustness.



# Interpolation
---
## Max gap length



### Player interpolations
* Relies on accurate identification, and reidentification. Errors in the tracking make very weird interpolations, where player bounding boxes are 
* Lowering the max gap length helps mitigate the tracking issues to a certain extent, but is kind of a work around. 
* Hard to balance, should be scaled with framerate
* 