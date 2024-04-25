_AI-Based Sports Highlight Generation for Social Media Cise Midoglu1,3, Saeed Shafiee Sabet1,3, Mehdi Houshmand Sarkhoosh2,3, Sayed Mohammad Majidi Dorcheh2,3, Sushant Gautam1,2, Tomas Kupka3, Pål Halvorsen1,2,3 1 SimulaMet, Norway 2 Oslo Metropolitan University, Norway 3 Forzasys, Norway Social media plays a significant role for sports organizations with millions of active fans [1-8], but social media publishing is often a tedious manual operation. With the development of AI, new tools are available for content generation and personalization to engage audiences [9-22]. We present an AI-based multimedia production pipeline for automatic soccer and ice hockey highlight sharing on social media, which ingests a broadcast (VoD / stream) and performs event detection, clipping, smart cropping (aspect ratio retargeting), thumbnail generation, summarization, and social media sharing_



# Overview
---

* Less detailed version of [[Forzify_pipeline]]
* Automatic pipeline for highlight sharing on social media
* Works for soccer and ice hockey
* Performs event detection, clipping, smart cropping, thumbnail generation, summarization, and social media sharing
* This paper does not include a lot of details, only **what** the pipeline does. It mentions some specific models/techniques.
* I have quoted this paper extensively in [[Project Description.pdf]], but not the details
* Pipeline consists of: Event detection, Clipping, Cropping, Thumbnail generation, Summarization, Sharing

# Testing/validation
* Pipeline is tested on content from Scandinavian soccer and ice hockey leagues, and they have run subjective user studies
* The studies show that an AI-based automated approach relying on advanced multimodal scene understanding facilitates social media engagement and increases quality of experience.


# Different models/techniques

## Event detection
* Challenges include high latency and low accuracy, problematic at the live edge
* Events include goals, cards, substitutions in real-time
* Detects events with high recall, low latency and accurate time estimation
* Detection is solely based on the visual modality, even though data includes sound
* Uses **3D convolutional neural networks**
* Tested on three datasets including **SoccerNet**


## Clipping
* Usually most time and expensive consuming operation, so important to automate
* Identifies appropriate event intervals, scene changes, game turnovers, logo transitions, cheering, and replays
* Utilizes scene boundary detection, logo detection, and optional cheering removal
* Experiment with different neural network architectures and present two models that have been evaluated both quantitatively and qualitatively with a user study

## Cropping
* **SmartCrop** is a tool for cropping to fit desired ratios based on different **POI**, with puck/ball being primary **POI**
* If ball/hockey puck is not visible, outlier detection and interpolation are used
	* average
	* IQR
	* Z-score
* Segments videos using the **TransNetV2** model and employs object detection through a custom **YOLOv8-medium** model, which has been retrained on a novel soccer and hockey dataset
* Interpolation techniques (linear, polynomial, ease-in-out, heuristic) are applied to enhance video quality and accuracy
* Frames are cropped either around POI or frames center, based on user preferences and POI visibility
* Before sharing, formats content to meet unique requirements of social media platforms, to ensure optimal viewing experience


## Thumbnail generation
