
# Video pre-processing
---

## Raw input
* `.mp4` or `.webm` videos
* Can be scraped from youtube using `yt-dlp`
* Compilation videos might be best, but also full matches (from Eliteserien?)

# Scene clipping
---
* The bounding box and homography transform pipeline works best with shorter video snippets, where each video is of one scene only
## pyscenedetect
* [pyscenedetect](https://www.scenedetect.com/) is a library to clip video into multiple shorter videos, based on camera shot changes/transitions.
### pyscenedetect detection methods
- **adaptive content scene detection** (`detect-adaptive`): uses rolling average of differences in HSL colorspace combined with thresholding to detect shot changes (fast cut)
	- Adaptive took (201 , 165)fps in normal mode and 60 fps in hq mode
- **content-aware scene detection** (`detect-content`): uses differences in HSL colorspace combined with filtering to detect shot changes (fast cut)
- **content-aware scene detection** (`detect-hash`): uses perceptual hashing to determine differences between frames to find shot changes (fast cut)
- **content-aware scene detection** (`detect-hist`): uses differences in histograms of Y channel of frames after conversion to YUV (fast cut)
- **threshold scene detection** (`detect-threshold`): uses average frame intensity (brightness) to detect slow transitions (fade in/out)


# Filter unwanted scenes - native approach
---
* We want to remove all clips which are not the standard zoomed out view from the side, or poorly detected clips
* After clipping we can assume that each video clip is similar for the object detection, therefore we can do a simple check for one of the frames to decide whether it likely is a videoclip we want to keep
* One approach is to run one of the frames through the player detection model, and then decide based on a few **critera**:
	* Are at least 4 players detected, within a given confidence threshold? **If not** it is likely not either zoomed out or of the pitch, and should **not be kept**
	* Are any of the player bounding boxes 1/3rd of the screen height? **If yes** this is likely a zoomed in shot, and should **not be kept**
* This seems promising, since the yolo model seems very consistant for player detection, especially for the expected view (side view)



# Linear interpolation
---
![[Pasted image 20250204152531.png]]
