<p style="font-size:25px;text-align:left"><b>Mars Rover Science Mission Navigation</b></p>

| Import folder     | Mars_rover  |
|:------------------|:------------|
| Action space      | Dict        |
| State space       | Dict        |



## Description
Multi-agent path finding (MAPF) problem, where agents starts from a some initial position, and should harvast as many minerals as possible. Each mineral is locatied randomly at the instatiation of the problem, and has different value. Agent dynamics in each axis is a second order integrator i.e., linear rate of change

for each agent the state vector is the position and velocity, and the action is the acceleration. The full state vector is the stacking of all agents’ states, and similarly for the actions. The reward is the total rewards collected from harvesting the mineral, minus the power consumption usued throughout the process.

## Action Space

| Action               | type              |   min.               |   max               |  Desc                         |
|:---------------------|:------------------|:---------------------|:--------------------|:------------------------------|
| power_x(drone)       | Box(1, float32)   |  -MAX_POWER(drone)   |  MAX_POWER(drone)   |  Acceleration in x axis       |
| power_y(drone)       | Box(1, float32)   |  -MAX_POWER(drone)   |  MAX_POWER(drone)   |     Acceleration in y axis    |
| harvest(drone)       | Discrete(2)       |     0                |   1                 |  Harvest if in mineral area   |

## Observation Space


| Import folder     | Mars_rover  |
|:------------------|:------------|
| Action space      | Dict        |
| State space       | Dict        |

## Rewards

## References




