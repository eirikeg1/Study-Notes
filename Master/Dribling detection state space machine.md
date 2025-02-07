
**# State Space Machine Algorithm for Dribble Detection**

## **Conceptual Overview**

The goal of this algorithm is to detect dribbling events in football (soccer) matches using a state-space model. The core concepts involve possession identification, spatial proximity zones, and event detection.

- **Controller**: Decides state transitions and manages logic flow.
- **Actuators**: Responsible for executing actions such as tracking possession, detecting players within zones, and maintaining event structures.

---

## **Definitions**

- **State Variables**: Define the current state of the system. Possible states are:
    
    - **Search State**
    - **Start Track State**
    - **Track State 1 (Close Proximity to Defender)**
    - **Track State 2 (Duel)**
    - **Detection State**
- **Input Variables**: Inputs to the system that drive state transitions, such as player positions, ball position, velocities, and distances.
    
- **Output Variables**: Outputs of the system, such as dribble event detections or player possession updates.
    
- **Actuators**: Functions that execute specific actions, such as calculating distances, updating possession, and logging events.
    

---

## **State-Space Definitions**

1. **State Variables**
    - **Search State (S1)**: System looks for the player closest to the ball and analyzes player proximity.
    - **Start Track State (S2)**: A dribbling event is initiated, and relevant data is recorded.
    - **Track State 1 (S3)**: System tracks player movement and defender proximity.
    - **Track State 2 (S4)**: System freezes possession updates and waits for player interactions.
    - **Detection State (S5)**: Possession checks are made to determine if a dribble or tackle has occurred.

2. **Input Variables**
    - **player_positions**: List of player coordinates.
    - **ball_position**: Current ball coordinate.
    - **player_velocities**: Velocity of each player.
    - **frame_number**: Current frame identifier.

3. **Output Variables**
    - **dribble_events**: List of dribble events detected, each with player ID, start frame, end frame, and defenders involved.

4. **Parameters**    
    - **outer_rad**: Defines the "outer" proximity radius.
    - **inner_rad**: Defines the "inner" close proximity radius.

5. **Actuators**
    - **Update Possession**: Identifies which player holds possession of the ball.
    - **Detect Proximity**: Checks which players are within inner and outer radius of the ball.
    - **Update Dribble Event**: Logs relevant information into the dribble event structure.
    - **Detect Defenders**: Identifies opposing players who are within range.

---

## **State Transitions**

**1. Search State (S1)**

- **Controller Logic**:
    1. Find the player closest to the ball.
    2. If the ball is within the player's **inner_rad**, move to **Start Track State (S2)**.
    3. If no defenders are found, stay in **Search State (S1)**.
    4. If defenders are within **inner_rad** or **outer_rad**, transition to **Start Track State (S2)**.
     
- **Actuators**:
    - Calculate distances between the ball and all players.
    - Identify defenders within **inner_rad** and **outer_rad**.

---

**2. Start Track State (S2)**
- **Controller Logic**:
    1. Log the start frame for the dribble event.
    2. Identify and store defenders within range.
    3. Initialize a **DribbleEvent** structure with the following attributes:
        - **possession holder**: Player ID with possession.
        - **start_frame**: Current frame.
        - **active_defenders**: List of player IDs of defenders within proximity.
    4. Move to **Track State 1 (S3)**.
    
- **Actuators**:
    - Log defenders within range.
    - Create a **DribbleEvent** object to store possession, start frame, and defender information.

---

**3. Track State 1 (S3)**
- **Controller Logic**:
    1. Update the frame list for the dribble event.
    2. Check for defenders entering **inner_rad**.
    3. If defenders enter **inner_rad**, move to **Track State 2 (S4)**.
    4. If possession changes or the ball leaves the **inner_rad**, cancel the dribble event and return to **Search State (S1)**.

- **Actuators**:
    - Update dribble event frame list.
    - Detect defenders within **inner_rad**.
    - Check possession change and ball-player distance.
---

**4. Track State 2 (S4)**
- **Controller Logic**:
    1. Freeze ball possession updates.
    2. Wait until only one player remains within **inner_rad**.
    3. If one player remains, transition to **Detection State (S5)**.

- **Actuators**
    - Detect player count in **inner_rad**.
    - Pause possession updates to avoid premature detection.

---

**5. Detection State (S5)**

- **Controller Logic**:
    1. Determine if possession has changed.
    2. If original possession holder retains possession, start a frame counter.
    3. If possession is held for a defined time window, mark the event as a **Dribble**.
    4. If possession shifts to a defender, detect a **Tackle** event.
    5. Log the dribble or tackle event.
    6. Return to **Search State (S1)**.

- **Actuators**:            
    - Detect possession changes.
    - Count frames for possession retention.
    - Record dribble or tackle event in the dribble event structure.

---

## **Event Structures**

**DribbleEvent**

```
DribbleEvent = {
  'possession_holder': PlayerID,
  'start_frame': FrameNumber,
  'end_frame': FrameNumber,
  'frames': [FrameNumbers],
  'active_defenders': [DefenderIDs]
}
```

---

## **Algorithm Flow**

1. **Initialize System**
    - Define **outer_rad** and **inner_rad**.
    - Initialize **DribbleEvent** structure.
2. **Start at Search State (S1)**
    - Use distance calculations to determine possession and proximity of defenders.
    - If conditions are met, transition to **Start Track State (S2)**.
3. **Enter Start Track State (S2)**
    - Log possession, defenders, and current frame as part of the dribble event.
    - Move to **Track State 1 (S3)**.
4. **Track Player Movement (S3)**
    - Monitor possession and proximity.
    - If a defender enters **inner_rad**, transition to **Track State 2 (S4)**.
5. **Duel State (S4)**
    - Pause possession updates and wait for one player to remain in **inner_rad**.
    - Transition to **Detection State (S5)**.
6. **Detect Events (S5)**
    - Determine if a **Dribble** or **Tackle** occurred.
    - Log event details.
    - Return to **Search State (S1)**.

---

This state-space machine effectively models a dribble detection system with precise transitions, input control, and output recording. By structuring the problem in this manner, it provides clarity, modularity, and robustness for live football match analysis.