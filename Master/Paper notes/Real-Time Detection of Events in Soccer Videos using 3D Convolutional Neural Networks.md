
# Summary

* [Link](https://home.simula.no/~paalh/publications/files/ism2020-olav.pdf)
* [[Real-Time Detection of Events in Soccer Videos using 3D Convolutional Neural Networks.pdf|PDF link]]
* Evaluated through baseline comparison from _SoccerNet_ in terms of both accuracy and tolerance for delays
* Results indicate that the current state of the art approach gives a higher detection accuracy if there is a higher tolerance for accurate time estimation, but proposed approach is better when real-time detection is required


## Abstract
_In this paper, we present an algorithm for automatically detecting events in soccer videos using 3D convolutional neural networks. The algorithm uses a sliding window approach to scan over a given video to detect events such as goals, yellow/red cards, and player substitutions. We test the method on three different datasets from SoccerNet, the Swedish Allsvenskan, and the Norwegian Eliteserien. Overall, the results show that we can detect events with high recall, low latency, and accurate time estimation. The trade-off is a slightly lower precision compared to the current state-of-the-art, which has higher latency and performs better when a less accurate time estimation can be accepted. In addition to the presented algorithm, we perform an extensive ablation study on how the different parts of the training pipeline affect the final results. Index Terms—Event detection, deep learning, sports analysis, soccer._


# Notes
---

* Current gold standard is manual work
* One especially useful scenario is live annotations, but today is often reliant on textual information which is not always available, and needs to process at the same speed as the video feed
* One approach is by spotting measuring the distances between the actual events and the predicted events
* Here we split Automatic event detection into two areas: **sports analytics** and **event detection**

## Sports analytics
* SoccerNet

## Action Detection
* Optical flow fields
* **Two-Stream Inflated 3d ConvNet** model, using both 3D convolution and the inception architecture.
	* One network for rgb and one for optical flow fields


## Ablation study
---

### Local behavior with sliding window
* From experiments it is not needed to sample too densely, which makes real-time easier

