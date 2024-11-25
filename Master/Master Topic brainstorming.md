


# Master topic
---
### Drible detection
* Drible opposite of tackle -> **if:** tackle and no possession change (no pass) **:** successful drible **else:** unsuccessful drible
* Check which player has possession before and after tackles -> if same player propose at drible
* Give a score of drible based of sound (commentary and crowd intensity)
* Dataset from youtube highlights
* From commentary?
* From external source?
	* Text commentary API
	* Webscraping
* Intensity of sound for ranking
* Calculations on 2d plane?
* GNN on 2d plane?
* First manual calculations on 2d coords, then proposed dataset manually filtered through
* **Contrastive learning**?

##### For selecting frames for input:
* Sliding window?
* Filter out frames where not enough homography points have a high enough confidence score (due to wrong type of scene, for example close up or video of bench/fans)
	* Extend homography model dataset for this scenario by adding this kind of images as well, without any annotations
* Use rule-based algorithm to automatically detect windows of varying sizes:
	* For example by looking at when defender enters and leaves a proximity zone around ball player
* 

### Mapping from camera to 2d coordinates
* Soccer net challenge 2024
* Perspective projection: Homography (mapping points from one flat surface to another)
* [python - Homography from football (soccer) field lines - Stack Overflow](https://stackoverflow.com/questions/60352448/homography-from-football-soccer-field-lines)
	* RANSAC to find lines, then do projection
* Kalman filters for time series?
	* Used to not have to calculate for every frame
	* Estimates if the current frame has same homography as previous

### Event detection
* [A Transformer-based System for Action Spotting in Soccer Videos](https://dl.acm.org/doi/pdf/10.1145/3552437.3555693) method for event detection, instead of TransNetv2?
	* First transformer for feature extraction, then CNN-based NetVLAD++ for classification
	* NetVLAD++: "state-of-the-art performances for action spotting on SoccerNet-v2"
	* Inductive bias of [[Week 4 - Convolutional Neural Networks |CNNs]]
* SoccerNet challenge results as inspiration
* Attention-based CNN?
* Graph Neural Networks
	* Mostly tactics/analytics, not event detection
	* [Event Detection in Football using Graph Convolutional Networks](https://arxiv.org/pdf/2301.10052)
* Sound
	* Multimodal model, or combination?
	* Stadium sounds, commentator
* Other?

### Concatenate tv camera to tactical view (overview camera)
* Tv camera for details, overview for game events/patterns

### Detect replays
* Compare player/ball positions for similar events
* Check similarity of pixels above a certain threshold? (Different camera angles problem)

### Data Preprocessing
* Extract movement traces?
* f
### Multimodal models
* VideoBERT
* MERLOT
* MM-VT
* OmniVL
* CLIP
* UNITER
* MM-VLN


# Ideas
---
* Sound and video
	* Commentator, fed into LLM?
	* Use background sound of fans to classify how interesting different events are?
	* Create embedding of both sound and video, concatenate and then classify?
* Ranking of classified event videos based on time limit (exactly 2 minutes)
	* For creating a summary of a designated time/length
	* 
* Event detection of unofficial events, like tackles and dribles
	* Detect dribles by unsuccessful tackles and no loss of possession from player?
* Mitigate problem of event detection false positive duplicates from replays, by analysing absolute player positions?
# Compute
---
* Simula cluster?
* [Machine Learning nodes from the AI HUB project - University of Oslo](https://www.uio.no/english/services/it/research/hpc/ml-noder/
* Fox?
* [NREC?](https://docs.nrec.no/intro.html)

