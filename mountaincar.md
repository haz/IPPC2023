<p style="font-size:25px;text-align:left"><b>Mountain car Control</b></p>

<div style="width:100%;text-align:center;">
  <a href="images/mountain_car.gif">
    <img src="images/mountain_car.gif" height="190" width="190" />
  </a>
</div>

|       |      |
|:------------------|:------------|
| Example name     | MountainCar |
| Action space      | Dict        |
| State space       | Dict        |

## Description
This domain is a recreation of the domain Mountain Car from the OpenAI Gym repositotry.

The Mountain Car MDP is a deterministic MDP that consists of a car placed stochastically at the bottom of a sinusoidal valley, with the only possible actions being the accelerations that can be applied to the car in either direction. The goal of the MDP is to strategically accelerate the car to reach the goal state on top of the right hill. There are two versions of the mountain car domain in gym: one with discrete actions and one with continuous. This version is the one with discrete actions.

This MDP first appeared in [Andrew Moore’s PhD Thesis (1990)](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-209.pdf)

## Constants (non-fluents)

| Constant     | Type             |  Desc                                               |
|:-------------|:-----------------|:----------------------------------------------------|
| GRAVITY_MAG  | float32          |  Force of gravity acting down                       |
| FORCE_MAG    | float32          |  Force applied to the side of the cart              |
| DEPTH        | float32          |  depth of the valley                                |
| MIN_POS      | float32          |  min position of cart                               |
| MAX_POS      | float32          |  max position of cart                               |
| MAX_VEL      | float32          |  max velocity of cart                               |
| GOAL_MIN     | float32          |  desired x position of cart                         |


All of these can be read from the RDDLEnv interface and from the RDDL files.

## Action Space

There is a single action taking {0, 1, 2} values, indicating if the cart should be pushed to the left or to the right or not at all.

| Action               | Type             |  Desc                                                  |
|:---------------------|:-----------------|:-------------------------------------------------------|
| action               | Discrete(3)      |  whether to accelerate left, none or right             |

If action is 0 then the cart is pushed to the left with FORCE_MAG force \
If action is 1 then no force is acting on the cart \
If action is 2 then the cart is pushed to the right with FORCE_MAG force 

- FORCE_MAG is available from the RDDLEnv interface and in the RDDL domain and instance.

## State Space

The state space represents the positions and velocities of all the drones in the problem, as well as the state of all the minearls in the domain.
The location and harvesting regions of the minearls are not part of the state, but are available through the non fluents in the problem.

| State             | Type                                   |  Desc                         |
|:------------------|:---------------------------------------|:------------------------------|
| pos               | Box(1, MIN_POS, MAX_POS, float32)      |  Cart position                |
| vel               | Box(1, -MAX_VEL, MAX_VEL, float32)     |  Cart velocity                |

- MIN_POS, MAX_POS and MAX_VEL are available from the RDDLEnv interface and in the RDDL domain and instance.

## Rewards
The goal is to reach the flag placed on top of the right hill as quickly as possible, as such the agent is penalised with a reward of -1 for each timestep.


## References
- [Mountain car example](https://github.com/ataitler/pyRDDLGym/tree/main/pyRDDLGym/Examples/MountainCar)
- Moore, A. W. (1990). Efficient memory-based learning for robot control.


<hr>
[Back to main page](index.md)
