# Dataset 1
---
* Based on dribble-comp-md.webm
* There were many replayed which were zoomed in, I ignored those, so only counted zoomed out clips, as the pipeline filters out zoomed clips
* 15 actual dribbles, 0 tackles
* /home/eirik/Projects/data/dribbling-detection-algorithm/comp-vid-md-2025-04-16

## Image coord runs
### Run 1
![[Pasted image 20250416174628.png]]
* detected 40 dribble events
* Manually approved:
	* 5 dribbles
	* 2 none
	* 0 tackles
* Many dribble events were split in two, and sometimes overlapping a bit, due to extra frames for each event

### Run 2
![[Pasted image 20250416195412.png]]
* Detected 8 dribbles
* Manually approved:
	* 6 dribbles
	* 2 none
	* 0 tackles

### Run 3
![[Pasted image 20250416210931.png]]

* Manually approved
	* 12 dribbles
	* 4 none
	* 0 tackles
### Run 4 
![[Pasted image 20250416211142.png]]

* Manually approved
	* 8 dribbles
	* 6 none

### Run 5
![[Pasted image 20250416214159.png]]
* Manually approved
	* 11 dribbles
	* 4 none
	* 0 tackles

## 2D coords

### Run 1
![[Pasted image 20250416203428.png]]
* Big problem with unstable 2d coordinates
* Manually approved
	* 9 dribbles
	* 8 none
	* 0 tackles

Example of unstable coords on two frames (4 frames between):
![[Pasted image 20250416203027.png|200]]
![[Pasted image 20250416203116.png|200]]

Another  example (7 between):
![[Pasted image 20250416203326.png|200]]
![[Pasted image 20250416203344.png|200]]



# Dataset 2
---

* Based on comp-vid-full.mpeg
* Note on compilation clips, that many of them end quite early/abruptly, so algorithm might not end properly

## No 2d

### Run 1
![[Pasted image 20250418141501.png]]

* Results
	* 34 dribbles
	* 4 tackles
	* 39 none

### Run 2
![[Pasted image 20250418145524.png]]

* Results
	* 73 dribbles
	* 1 tackle
	* 76 none



### Run 3
![[Pasted image 20250418151129.png]]

* Results
	* 89 dribbles
	* 1 tackle
	* 58 none

Image below shows example of radii sizes, as well as another example of why using 2d coordinates might not be the best way
![[Pasted image 20250418151120.png]]


### Run 4
![[Pasted image 20250418152205.png]]

* Results
	* 68 dribbles
	* 1 tackles
	* 26 none


### Run 3
![[Pasted image 20250418154338.png]]

* Results 1
	* 98 dribbles
	* 1 tackles
	* 30 none
* Results 2 (Used) 9m 11s
	* 101
	* 1
	* 26

Example with 2 balls on the pitch
![[Pasted image 20250418154316.png]]

Example with 3 balls on the pitch
![[Pasted image 20250418154911.png]]




