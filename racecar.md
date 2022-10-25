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

A race car is required to reach a target from an initial position. The race car is described as a kinematic 2nd order model. The race track is bounded with lines representing the track bounds, hitting one of the bounds is considered a failure and the episode is terminated. The shape of the track is represented by a series of point conected with lines.

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

The actioins are the force (or acceleartion in a kinematic setting) applied to each movement axis of the race car.

| Action               | Type             |  Desc                                                  |
|:---------------------|:-----------------|:-------------------------------------------------------|
| fx               | BOX(1, -MAX-F, MAX-F, float32)      |  x force component applied to the car             |
| fy               | BOX(1, -MAX-F, MAX-F, float32)      |  y force component applied to the car             |


- MAX-F is available from the RDDLEnv interface and in the RDDL domain and instance.

## State Space

The state space is the positions and velocities of the race car in both axis.

| State             | Type                                   |  Desc                         |
|:------------------|:---------------------------------------|:------------------------------|
| x               | Box(1, -inf, inf, float32)      |  x position of car                |
| y               | Box(1, -inf, inf, float32)     |  y position of car                |
| vx               | Box(1, inf, inf, float32)      |  c velocity of car                |
| vy               | Box(1, -inf, inf, float32)     |  y velocity of car                |



## Rewards

The reward of this domain is the minus the cost of using the engines (min power cost) plus the goal reward if the agent reaches the goal


<hr>
[Back to main page](index.md)
