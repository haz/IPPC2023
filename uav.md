
<p style="font-size:25px;text-align:left"><b>Multi-UAV Trajectory Planning</b></p>

<div style="width:100%;text-align:center;">
  <a href="images/drones.gif">
    <img src="images/drones.gif" height="190" width="190" />
  </a>
</div>

|       |      |
|:------------------|:------------|
| Import folder     | drone_**      |
| Action space      | Dict        |
| State space       | Dict        |

** stand for con, dis, mix.


## Description

A UAV fleet, described by first order constrained dynamics, are required to reach a goal position in the x-y-z space from thier initial position.
The UAV are represented by their 6 positional coordinates (cartesian coordinates and angles), and the velocity in the direction of the nose. The velocity is a first order integrator, i.e., integration over the acceleration, while the angles are assumed to be also first order integrator, i.e., small directe changes to the angles are assumed to be possible. The goal is to navigate the drones to the goal location. Note that some of the drones are not controllable! and so are there but nothing we do can affect them!

This domain has three version! 
1. Fully continuous, angles and velocity/acceleration are real bounded numbers.
2. Fully discrete, angles and velocity/acceleration are bounded integers.
3. Hybrid, i.e., Mix Discrete-continuous, angles are bounded integers and the velocity/acceleration is a real number.

## Constants (non-fluents)

| Constant                 | Type             |  Desc                                               |
|:-------------------------|:-----------------|:----------------------------------------------------|
| CONTROLLABLE(aircraft)   | float32          |  Whether an aircraft is contrallable                |
| GRAVITY                  | float32          |  Earth gravity acceleration coefficient             |
| MIN_X                    | float32          |  Min X of the space                                 |
| MAX_X                    | float32          |  Max X of the space                                 |
| MIN_Y                    | float32          |  Min Y of the space                                 |
| MAX_Y                    | float32          |  Max X of the space                                 |
| MIN_Z                    | float32          |  Min Z of the space                                 |
| MAX_Z                    | float32          |  Max X of the space                                 |
| SCALE_FACTOR             | float32          |  Time scale factor for dynamic equations (Delta T)  |
| RANDOM_WALK_COEFF        | float32          |  RAndom walk var of the non contrallable aircrafts  |
| VEL_REG                  | float32          |  Velocity regularization (prevent division by zero  |
| MIN_ACC(aircraft)        | float32          |  Minmum acceleration value                          |
| MAX_ACC(aircraft)        | float32          |  Maximum acceleration value                         |
| MIN_PHI(aircraft)        | float32          |  Minimum phi change in the single time step         |
| MAX_PHI(aircraft)        | float32          |  Maximum phi change in the single time step         |
| MIN_THETA(aircraft)      | float32          |  Minimum theta change in the single time step       |
| MAX_THETA(aircraft)      | float32          |  Maximum thera change in the single time step       |
| GOAL_X(aircraft)         | float32          |  Aircraft's goal X position                         |
| GOAL_Y(aircraft)         | float32          |  Aircraft's goal Y position                         |
| GOAL_Z(aircraft)         | float32          |  Aircraft's goal Y position                         |


All of these can be read from the RDDLEnv interface and from the RDDL files.


## Action Space

The actions are the acceleration in the direction of the nose, and the small changes to the roll and pitch angles.

#### continuous

| Action               | type             |  Desc                          |
|:---------------------|:-----------------|:-------------------------------|
| set_acc(aircraft)    | Box(1, MIN_ACC(aircraft), MAX_ACC(aircraft), np.float32)  |  Propelling force to apply to the aircraft |
| set_phi(aircraft)    | Box(1, MIN_PHI(aircraft), MAX_PHI(aircraft), np.float32)  |  Roll angle change  |
| set_theta(aircraft)  | Box(1, MIN_THETA(aircraft), MIN_THETA(aircraft), np.float32)  |  Pitch angle change  |

#### Discrete 

| Action               | type             |  Desc                          |
|:---------------------|:-----------------|:-------------------------------|
| set_acc(aircraft)    | Discrete(MAX_ACC(aircraft)+MIN_ACC(aircraft)+1, start=MIN_ACC(aircraft))  |  Propelling force to apply to the aircraft |
| set_phi(aircraft)    | Discrete(MAX_PHI(aircraft)+MIN_PHI(aircraft)+1, start=MIN_PHI(aircraft))  |  Roll angle change  |
| set_theta(aircraft)  | Discrete(MAX_THETA(aircraft)+MIN_THETA(aircraft)+1, start=MIN_THETA(aircraft))  |  Pitch angle change  |

#### Hybrid

| Action               | type             |  Desc                          |
|:---------------------|:-----------------|:-------------------------------|
| set_acc(aircraft)    | Box(1, MIN_ACC(aircraft), MAX_ACC(aircraft), np.float32)  |  Propelling force to apply to the aircraft |
| set_phi(aircraft)    | Discrete(MAX_PHI(aircraft)+MIN_PHI(aircraft)+1, start=MIN_PHI(aircraft))  |  Roll angle change  |
| set_theta(aircraft)  | Discrete(MAX_THETA(aircraft)+MIN_THETA(aircraft)+1, start=MIN_THETA(aircraft))  |  Pitch angle change  |

- MIN_ACC(aircraft), MAX_ACC(aircraft), MIN_PHI(aircraft), MAX_PHI(aircraft), MIN_THETA(aircraft) and MIN_THETA(aircraft) are available from the RDDLEnv interface and in the RDDL domain and instance.

## State Space

The state space represents the position and angles of each UAV, and also the velocity in the direction of the nose.

| State                      | type              |  Desc                                   |
|:---------------------------|:------------------|:----------------------------------------|
| pos_x(aircraft)             |  Box(1, MIN_X, MAX_X, np.float32)  | Position of the UAV in the x axis |
| pos_y(aircraft)             |  Box(1, MIN_Y, MAX_Y, np.float32)  | Position of the UAV in the y axis |
| pos_z(aircraft)             |  Box(1, MIN_Z, MAX_Z, np.float32)  | Position of the UAV in the z axis |
| theta(aircraft)             |  Box(1, -inf, inf, np.float32)  | The UAV's pitch angle |
| phi(aircraft)               |  Box(1, -inf, inf,  np.float32)  | The UAV's roll angle |
| psi(aircraft)               |  Box(1, -inf, inf,  np.float32)  | The UAV's yaw angle |
| vel(aircraft)               |  Box(1, -inf, inf,  np.float32)  | UAV's velocity in the direction of the nose |

- MIN_X, MAX_X, MIN_Y, MAX_Y, MIN_Z and MAX_Z are available from the RDDLEnv interface and in the RDDL domain and instance.

## Rewards

The reward function is defined as 

The sum of the norm-2 distance of all the *controllable* drones.

## References

- David G. Hull. 2007. Fundamentals of Airplane Flight Mechanics (2nd ed.).
Springer.


<hr>
[Back to main page](index.md)
