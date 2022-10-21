<p style="font-size:25px;text-align:left"><b>Elevator Planning During Evening Rush Hour</b></p>

<div style="width:100%;text-align:center;">
  <a href="images/elevator2.gif">
    <img src="images/elevator2.gif" height="190" width="190" />
  </a>
</div>

|       |      |
|:------------------|:------------|
| Import folder     | Elevator  |
| Action space      | Dict        |
| State space       | Dict        |



## Description

The Elevator domain models evening rush hours when people from different floors in a building want to go down to the bottom floor using elevators. 
Potential passengers arrive at a floor according to the Poisson process, with specific rates that can be different across different floors. 
An elevator can move upwards to pick up passengers; once it opens its door to let people in, it can only move down towards the bottom floor,
though the elevator can stop at intermediate floors to pick up more passengers.

Per each person in an elevator, there is a small penalty in rewards.  Additionally, there is a penalty for each person waiting for an elevator.  
When an elevator delivers a passenger to their destination, a large positive reward is given per person. 
So, a good policy should be able to minimize the penalties while maximizing the positive rewards by delivering many people so that they can go back home!

## Constants (non-fluents)

ARRIVE-PARAM(floor) float32 The rate of Poisson arrival process
TOP-FLOOR(floor) bool Indicator for the top floor
BOTTOM-FLOOR(floor) bool Indicator for the bottom floor
ADJACENT-UP(floor, floor) bool Indicator for adjacent floors
PRECEDENCE(elevator, elevator) bool Which elevator takes precedence over the other
IN-ELEVATOR-PENALTY float32 Penalty for people in elevators
PEOPLE-WAITING-PENALTY float32 Penalty for people waiting on floors
REWARD-DELIVERED float32 Reward for delivering each person to the bottom floor


| Constant                       | Type             |  Desc                                                    |
|:-------------------------------|:-----------------|:---------------------------------------------------------|
| ARRIVE-PARAM(floor)            | float32          |   The rate of Poisson arrival process                    |
| TOP-FLOOR(floor)               | bool             |   Indicator for the top floor                            |
| BOTTOM-FLOOR(floor)            | bool             |   Indicator for the bottom floor                         |
| ADJACENT-UP(floor, floor)      | bool             |   Indicator for adjacent floors                          |
| PRECEDENCE(elevator, elevator) | float32          |   Which elevator takes precedence over the other         |
| IN-ELEVATOR-PENALTY            | float32          |   Penalty for people in elevators                        |
| PEOPLE-WAITING-PENALTY         | float32          |   Penalty for people waiting on floors                   |
| REWARD-DELIVERED               | float32          |   Reward for delivering each person to the bottom floor  |

All of these can be read from the RDDLEnv interface and from the RDDL files.

## Action Space

The actions are the elevator control operations.

| Action                     | Type             |  Desc                                                                             |
|:---------------------------|:-----------------|:----------------------------------------------------------------------------------|
| move-current-dir(elevator) | Discrete(2)      |  Whether to move in the current direction (cannot move if door is open)           |
| open-door(elevator)        | Discrete(2)      |  Whether to open the door to let people in (direction changes to down afterwards) |
| close-door(elevator)       | Discrete(2)      |  Whether to close door                                                            |


## State Space

he state space represents the temerature and the previous production of each of the plants in the problem.

| State                               | Type         |  Desc                                          |
|:------------------------------------|:-------------|:-----------------------------------------------|
| num-person-waiting(floor)           | int          | Number of people waiting on a floor            |
| num-person-in-elevator(elevator)    | int          | Number of people in an elevator                |
| elevator-dir-up(elevator)           | bool         | Direction of an elevator (True if going up)    |
| elevator-closed(elevator)           | bool         | Whether the door is open or closed             |
| elevator-at-floor(elevator,floor)   | bool         | Whether an elevator is on a specific floor     |               



## Rewards

$r_t = - p_e * \sum_{e \in elevators} num-person-in-elevator(e) - p_w * \sum_{f \in floors} num-person-waiting(f) + rew * \sum_{e \in elevators} (num-person-in-elevator(e) * I_bottom(e))$

where,

- p_e: IN-ELEVATOR-PENALTY
- p_w: PEOPLE-WAITING-PENALTY
- rew: REWARD-DELIVERED
- I_bottom(e): 1 if e is at the bottom floor; otherwise, 0

<!--## References -->


<hr>
[Back to main page](index.md)

