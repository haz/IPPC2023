<p style="font-size:25px;text-align:left"><b>Race Car Control</b></p>

<div style="width:100%;text-align:center;">
  <a href="images/racecar.gif">
    <img src="images/racecar.gif" height="190" width="190" />
  </a>
</div>

|       |      |
|:------------------|:------------|
| Import folder     | MountainCar |
| Action space      | Dict        |
| State space       | Dict        |

## Description


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


## References


<hr>
[Back to main page](index.md)
