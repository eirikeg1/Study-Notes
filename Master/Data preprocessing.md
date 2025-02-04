
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




# Linear interpolation
---
![[Pasted image 20250204152531.png]]