
<p style="font-size:25px;text-align:left"><b>Multi-UAV Trajectory Planning</b></p>

<div style="width:100%;text-align:center;">
  <a href="images/Rpowergen_static.png">
    <img src="images/powergen_static.png" height="190" width="190" />
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

## Action Space

The actions are the acceleration in the direction of the nose, and the small changes to the roll and pitch angles.

#### continuous

| Action               | type             |  Desc                          |
|:---------------------|:-----------------|:-------------------------------|
| set_acc(aircraft)    | Box(1, np.float32)  |  Propelling force to apply to the aircraft |
| set_phi(aircraft)    | Box(1, np.float32)  |  Roll angle change  |
| set_theta(aircraft)  | Box(1, np.float32)  |  Pitch angle change  |

#### Discrete 

| Action               | type             |  Desc                          |
|:---------------------|:-----------------|:-------------------------------|
| set_acc(aircraft)    | Discrete()  |  Propelling force to apply to the aircraft |
| set_phi(aircraft)    | Discrete()  |  Roll angle change  |
| set_theta(aircraft)  | Discrete  |  Pitch angle change  |

#### Hybrid

| Action               | type             |  Desc                          |
|:---------------------|:-----------------|:-------------------------------|
| set_acc(aircraft)    | Box(1, np.float32)  |  Propelling force to apply to the aircraft |
| set_phi(aircraft)    | Discrete()  |  Roll angle change  |
| set_theta(aircraft)  | Discrete  |  Pitch angle change  |


## State Space

The state space represents the position and angles of each UAV, and also the velocity in the direction of the nose.

| State                      | type              |  Desc                                   |
|:---------------------------|:------------------|:----------------------------------------|
| pos_x(aircraft)             |  Box(1, np.float32)  | Position of the UAV in the x axis |
| pos_y(aircraft)             |  Box(1, np.float32)  | Position of the UAV in the y axis |
| pos_z(aircraft)             |  Box(1, np.float32)  | Position of the UAV in the z axis |
| theta(aircraft)             |  Box(1, np.float32)  | The UAV's pitch angle |
| phi(aircraft)               |  Box(1, np.float32)  | The UAV's roll angle |
| psi(aircraft)               |  Box(1, np.float32)  | The UAV's yaw angle |
| vel(aircraft)               |  Box(1, np.float32)  | UAV's velocity in the direction of the nose |


## Rewards

The reward function is defined as 

The sum of the norm-2 distance of all the *controllable* drones.

## References

- David G. Hull. 2007. Fundamentals of Airplane Flight Mechanics (2nd ed.).
Springer.



