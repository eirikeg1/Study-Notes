

# Initial dataset

The dataset is the 2025 soccernet game state recognition challenge. This includes videos annotated with: Player 2d positions (relative to homographical pitch)
[Link to repo](https://github.com/SoccerNet/sn-gamestate)


# Algorithm
_Currently just dribbling, not tackling_

## Initial setup
1. Pick a player radius as the outer radius (outer_rad)
	* Should this be percentage based? How about zoomed in videos?
	* **Could the homography transformation be used to estimate distance?**
2. Pick a ball radius as the inner radius (inner_rad)
3. Create a structure to keep track of current track
	* Possession holder
	* Start frame, End frame
	* All frame numbers
	* Active defenders (list of ids)

## Algorithm
### Search state
1. Find the closest player to the ball
2. Is the ball within inner_rad of this player?
	* Set possession holder to player_id
3.  Is there an opposition player within inner_rad or outer_rad?
	* If yes:  go to [[#Track state 1]].
	* If no: **go to next frame**, back to [[#Search state]].

### Start track state
1. Set current frame to start frame
2. Go to [[#Track state 1]]

### Track state 1
1. Is the current   
2. Add current frame to 
3. Add closest defender to active defenders
