
# TODO
* Test dribbling detection algorithm:
	* Test on smaller subset where you know videos are mislabeled or misclassified
	* With all entities converted to players (maybe except for "other")
	* Without team differentiation
	* Compare longer/shorter videos

# Player object detection
---
* High quality bounding box predictions
* Low quality object class on external datasets
	* Goalkeeper, referee, player, other is often problematic
		* ![[Pasted image 20250128180418.png]]
	* Referee overfits on yellow shirt and black shorts
		* ![[Pasted image 20250128173945.png]]

## YOLO model training
* Gradually improving
* When training on player and ball:
* **For future research:**
	* Fine tune model on different data
	* Specialized model for predicting ball


### After about 25 epochs
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