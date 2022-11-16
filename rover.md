<p style="font-size:25px;text-align:left"><b>Mars Rover Science Mission Navigation</b></p>

<div style="width:100%;text-align:center;">
  <a href="images/Rover_image2.gif">
    <img src="images/Rover_image2.gif" height="190" width="190" />
  </a>
</div>

|       |      |
|:------------------|:------------|
| Example name      | MarsRover   |
| Action space      | Dict        |
| State space       | Dict        |


## Description
Multi-agent path finding (MAPF) problem, where agents starts from a some initial position, and should harvast as many minerals as possible. Each mineral is locatied randomly at the instatiation of the problem, and has different value. Agent dynamics in each axis is a second order integrator i.e., linear rate of change

for each agent the state vector is the position and velocity, and the action is the acceleration. The full state vector is the stacking of all agents’ states, and similarly for the actions. The reward is the total rewards collected from harvesting the mineral, minus the power consumption usued throughout the process.

## Constants (non-fluents)

| Constant                 | Type             |  Desc                                               |
|:-------------------------|:-----------------|:----------------------------------------------------|
| MAX-POWER(drone)         | float32          |  Norm upper bound constraint on the power inputs    |
| SCALE-FACTOR             | float32          |  Time scale factor for dynamic equations (Delta T)  |
| MINERAL-AREA(mineral)    | float32          |  Mineral harvesting radius area                     |
| MINERAL-VALUE(mineral)   | float32          |  Mineral harvest value                              |
| MINERAL-POS_X(mineral)   | float32          |  Mineral X position                                 |
| MINERAL-POS_XY(mineral)  | float32          |  Mineral Y position                                 |

All of these can be read from the RDDLEnv interface and from the RDDL files.

## Action Space

The actions are the forces operating on the drones by their motors in the *x* and *y* axes (decoupled model), and a harvest action that can be applied by a drone if it is in a mineral harvest region, the result of the harvest action if applicable is that the mineral is harvested, and cannot be harvested again.

| Action               | Type             |  Desc                          |
|:--------------------|:-----------------|:-------------------------------|
| power-x(drone)      | Box(1, -MAX_POWER(drone), MAX_POWER(drone), float32)   |  Propelling force in x axis    |
| power-y(drone)      | Box(1, -MAX_POWER(drone), MAX_POWER(drone), float32)   |     Propelling force in y axis |
| harvest(drone)      | Discrete(2)       |  Harvest if in mineral area    |

- MAX_POWER(drone) is available from the RDDLEnv interface and in the RDDL domain and instance.

## State Space

The state space represents the positions and velocities of all the drones in the problem, as well as the state of all the minearls in the domain.
The location and harvesting regions of the minearls are not part of the state, but are available through the non fluents in the problem.

| State                      | Type              |  Desc                                   |
|:---------------------------|:------------------|:----------------------------------------|
| pos-x(drone)               | Box(1, -np.inf, np.inf, float32)   | Position in x axis                      |
| vel-x(drone)               | Box(1, -np.inf, np.inf, float32)   |  Velocity in x axis                     |
| pos-y(drone)               | Box(1, -np.inf, np.inf, float32)   |  Position in y axis                     |
| vel-y(drone)               | Box(1, -np.inf, np.inf, float32)   |  Velocity in y axis                     |
| mineral_harvested(mineral) | Discrete(2)       |  True if the minearl was not harvested  |

## Rewards

The reward function is defined as 

$$r_t = \sum_{d \in drones} -power-x(d)^2 - power-y(d)^2 - harvest-action(d) + harvest(d,m) $$ 

where, 
- $power-x(d)$ - is the current force in the x axis of drone *d*.
- $power-y(d)$ - is the current force in the y axis of drone *d*.
- $harvest-action(d)$ - is the cost of harvesting.
- $harvest(d)$ - is reward for succesfully harvesting mineral *m* by drone *d*.


## References
- [Mars rover example](https://github.com/ataitler/pyRDDLGym/tree/main/pyRDDLGym/Examples/Mars_rover)

<hr>
[Back to main page](index.md)

