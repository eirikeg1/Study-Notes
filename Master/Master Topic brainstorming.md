

# Master topic
---
## Event detection
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

## Detect replays
* Compare player/ball positions for similar events
* Check similarity of pixels above a certain threshold? (Different camera angles problem)
## Drible detection
* Drible opposite of tackle -> **if:** tackle and no possession change (no pass) **:** successful drible **else:** unsuccessful drible
* Check which player has possession before and after tackles -> if same player propose at drible
* Give a score of drible based of sound (commentary and crowd intensity)

## Data Preprocessing
* Extract movement traces?
* f
## Multimodal models
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

