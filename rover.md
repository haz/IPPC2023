<p style="font-size:25px;text-align:left"><b>Mars Rover Science Mission Navigation</b></p>


|:------------------|:------------|
| Action space      | Dict        |
| State space       | Dict        |
| Import folder     | Mars_rover  |
|:------------------|:------------|


## Description
Multi-agent path finding (MAPF) problem, where agents starts from a some initial position, and should harvast as many minerals as possible. Each mineral is locatied randomly at the instatiation of the problem, and has different value. Agent dynamics in each axis is a second order integrator i.e., linear rate of change

for each agent the state vector is the position and velocity, and the action is the acceleration. The full state vector is the stacking of all agents’ states, and similarly for the actions. The reward is the total rewards collected from harvesting the mineral, minus the power consumption usued throughout the process.

## Action Space

## Observation Space

## Rewards

## References




