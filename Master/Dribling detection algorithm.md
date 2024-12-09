
# Initial dataset

The dataset is the 2025 soccernet game state recognition challenge. This includes videos annotated with: Player 2d positions (relative to homographical pitch)
[Link to repo](https://github.com/SoccerNet/sn-gamestate)

## Short conceptual explanation
1. Possession Identification
	- First step: Tag the player closest to the ball
	- Proximity-based possession determination
	- Closest player
	- Perhaps extend to use players velocity? Player with possession and/or defender
	- Change size of proximity when a lot of players are around?

2. Proximity Zones Strategy: two-zone approach (inner_rad and outer_rad)
	- Handles coordinate inaccuracies
	- Creates a "spatial interaction" detection mechanism
	- Provides multiple states for action detection
	- Detection is done once one of the players exits either inner or outer rad (to be tuned)

3. Detections:
	* Drible: when the original possession holder still has possession after apponent "attack", for a set time (minimal time to prevent passing actions from being detected)
	* Tackle: If "attacking" player gets possession of the ball

# Algorithm
_Currently just dribbling, not tackling_

## Initial setup
1. Pick a player radius as the outer radius (outer_rad)
	* Should this be percentage based? How about zoomed in videos?
	* **Could the homography transformation be used to estimate distance?**
2. Pick a ball radius as the inner radius (inner_rad)
3. Create a structure to keep track of dribbling events (**DribleEvent**)
	* **Possession holder**
	* **Start frame, End frame**
	* **All frame numbers**
	* **Active defenders** (list of ids)

## Algorithm
### Search state
1. Find the closest player to the ball
2. Is the ball within inner_rad of this player?
	* Set possession holder to player_id
3.  Is there an opposition player within inner_rad or outer_rad?
	* If yes:  go to [[#Track state 1]].
	* If no: **go to next frame**, back to [[#Search state]].

### Start track state
1. Set start frame to current frame
2. Add defenders within range to **active defenders**
3. Go to [[#Track state 1]] and create a **DribleEvent**

### Track state 1
1. Add current frame to all frame numbers in **DribleEvent**
2. Add closest defender to active defenders
3. If possession state has changed (new player, or player too far from ball), delete **DribleEvent** and go to [[#Search state]]
4. If any player from the opponent team enters inner_rad, go to [[#Track state 2]], else jump to 1. in current state

### Track state 2
1. Stop updating ball possession holder while in this state
2. Repeat this state until there is only one player within inner_rad, then go to [[#Detection state]]

### Detection state
1. Check what player is the possession holder (by id):
	* If the same player as from [[#Start track state]] has the ball, start a timer/count frames with possession. If player has possession long enough, detect a **Drible**
	* If a opponent which was in either inner_rad or outer_rad has possession, detect a **Tackle**
	* Else: do nothing
2. If a detection was made, save it. If not delete the event object
3. Go to [[#Search state]]

