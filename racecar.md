<p style="font-size:25px;text-align:left"><b>Race Car Control</b></p>

<div style="width:100%;text-align:center;">
  <a href="images/racecar.gif">
    <img src="images/racecar.gif" height="190" width="190" />
  </a>
</div>

|       |      |
|:------------------|:------------|
| Import folder     | RaceCar     |
| Action space      | Dict        |
| State space       | Dict        |

## Description


## Constants (non-fluents)

| Constant     | Type             |  Desc                                               |
|:-------------|:-----------------|:----------------------------------------------------|
| X1(b)        | float32          |  boundary is the line segment (X1, Y1) -> (X2, Y2)  |
| Y1(b)        | float32          |  boundary is the line segment (X1, Y1) -> (X2, Y2)  |
| X2(b)        | float32          |  boundary is the line segment (X1, Y1) -> (X2, Y2)  |
| Y2(b)        | float32          |  boundary is the line segment (X1, Y1) -> (X2, Y2)  |
| X0           | float32          |  starting x position of car |
| Y0           | float32          |  starting y position of car   |
| GX           | float32          |  x center of goal region       |
| GY           | float32          |  y center of goal region                            |
| RADIUS      | float32          |  radius of goal region                               |
| COST      | float32          |  cost of fuel, proportional to force                               |
| GOAL_REWARD      | float32          |  reward upon reaching the goal region                               |
| MAX-F      | float32          |  maximum force in each direction                               |
| MASS      | float32          |  mass of the car                               |
| DT      | float32          |  rhow much time passes between epochs                               |



All of these can be read from the RDDLEnv interface and from the RDDL files.

## Action Space

There is a single action taking {0, 1, 2} values, indicating if the cart should be pushed to the left or to the right or not at all.

| Action               | Type             |  Desc                                                  |
|:---------------------|:-----------------|:-------------------------------------------------------|
| fx               | BOX(1, -MAX-F, MAX-F, float32)      |  x force component applied to the car             |
| fy               | BOX(1, -MAX-F, MAX-F, float32)      |  y force component applied to the car             |


- MAX-F is available from the RDDLEnv interface and in the RDDL domain and instance.

## State Space

The state space represents the positions and velocities of all the drones in the problem, as well as the state of all the minearls in the domain.
The location and harvesting regions of the minearls are not part of the state, but are available through the non fluents in the problem.

| State             | Type                                   |  Desc                         |
|:------------------|:---------------------------------------|:------------------------------|
| x               | Box(1, -inf, inf, float32)      |  x position of car                |
| y               | Box(1, -inf, inf, float32)     |  y position of car                |
| vx               | Box(1, inf, inf, float32)      |  c velocity of car                |
| vy               | Box(1, -inf, inf, float32)     |  y velocity of car                |



## Rewards


## References


<hr>
[Back to main page](index.md)
