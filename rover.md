<p style="font-size:25px;text-align:left"><b>Mars Rover Science Mission Navigation</b></p>

<a href="images/Rover_image.gif">
        <p style="text-align:center">
                <img src="images/Rover_image.gif" height="190" width="190" />
        </p>
</a>

|       |      |
|:------------------|:------------|
| Import folder     | Mars_rover  |
| Action space      | Dict        |
| State space       | Dict        |


## Description
Multi-agent path finding (MAPF) problem, where agents starts from a some initial position, and should harvast as many minerals as possible. Each mineral is locatied randomly at the instatiation of the problem, and has different value. Agent dynamics in each axis is a second order integrator i.e., linear rate of change

for each agent the state vector is the position and velocity, and the action is the acceleration. The full state vector is the stacking of all agents’ states, and similarly for the actions. The reward is the total rewards collected from harvesting the mineral, minus the power consumption usued throughout the process.

## Action Space

The actions are the forces operating on the drones by their motors in the *x* and *y* axes (decoupled model), and a harvest action that can be applied by a drone if it is in a mineral harvest region, the result of the harvest action if applicable is that the mineral is harvested, and cannot be harvested again.

| Action               | type             |  Desc                          |
|:---------------------|:-----------------|:-------------------------------|
| power_x(drone)      | Box(1, float32)   |  Propelling force in x axis    |
| power_y(drone)      | Box(1, float32)   |     Propelling force in y axis |
| harvest(drone)      | Discrete(2)       |  Harvest if in mineral area    |

## State Space

The state space represents the positions and velocities of all the drones in the problem, as well as the state of all the minearls in the domain.
The location and harvesting regions of the minearls are not part of the state, but are available through the non fluents in the problem.

| State                      | type              |  Desc                                   |
|:---------------------------|:------------------|:----------------------------------------|
| pos_x(drone)               | Box(1, float32)   | Position in x axis                      |
| vel_x(drone)               | Box(1, float32)   |  Velocity in x axis                     |
| pos_y(drone)               | Box(1, float32)   |  Position in y axis                     |
| vel_y(drone)               | Box(1, float32)   |  Velocity in y axis                     |
| mineral_harvested(mineral) | Discrete(2)       |  True if the minearl was not harvested  |

## Rewards

The reward function is defined as 

$$r_t = \sum_{d \in drones} -power_x(d)^2 - power_y(d)^2 - harvest\_action(d) + harvest(d,m) $$ 

where, 
- $power_x(d)$ - is the current force in the x axis of drone *d*.
- $power_y(d)$ - is the current force in the y axis of drone *d*.
- $harvest\_action(d)$ - is the cost of harvesting.
- $harvest(d)$ - is reward for succesfully harvesting mineral *m* by drone *d*.


## References




