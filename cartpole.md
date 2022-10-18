<p style="font-size:25px;text-align:left"><b>Mars Rover Science Mission Navigation</b></p>

<div style="width:100%;text-align:center;">
  <a href="images/cart_pole.gif">
    <img src="images/cart_pole.gif" height="190" width="190" />
  </a>
</div>

|       |      |
|:------------------|:------------|
| Import folder     | Cartpole    |
| Action space      | Dict        |
| State space       | Dict        |


## Description
This environment corresponds to the version of the cart-pole problem described by Barto, Sutton, and Anderson 
in “[Neuronlike Adaptive Elements That Can Solve Difficult Learning Control Problem](https://ieeexplore.ieee.org/document/6313077)”.
A pole is attached by an un-actuated joint to a cart, which moves along a frictionless track. 
The pendulum is placed upright on the cart and the goal is to balance the pole by applying forces in the left and right direction on the cart.

## Constants (non-fluents)

| Constant     | Type             |  Desc                                               |
|:-------------|:-----------------|:----------------------------------------------------|
| GRAVITY      | float32          |  force of gravity acting down                       |
| FORCE_MAG    | float32          |  force applied to the side of the cart              |
| CART_MASS    | float32          |  Mass of the cart                                   |
| POLE_MASS    | float32          |  Mass of the pole                                   |
| POLE_LEN     | float32          |  Half of the pole length                            |
| TIME_STEP    | float32          |  Seconds between state updates                      |
| POS_LIMIT    | float32          |  Limit of cart position                             |
| ANG_LIMIT    | float32          |  Limit of pole angle                                |

All of these can be read from the RDDLEnv interface and from the RDDL files.

## Action Space

The actions are the forces operating on the drones by their motors in the *x* and *y* axes (decoupled model), and a harvest action that can be applied by a drone if it is in a mineral harvest region, the result of the harvest action if applicable is that the mineral is harvested, and cannot be harvested again.

| Action               | Type             |  Desc                                                  |
|:---------------------|:-----------------|:-------------------------------------------------------|
| force_side           | Discrete(2)      |  whether to apply force to left, right side or none    |

If force_side is 0 then the cart is pushed to the left with FORCE_MAG force \
If force_side is 1 then the cart is pushed to the right with FORCE_MAG force 

- FORCE_MAG is available from the RDDLEnv interface and in the RDDL domain and instance.

## State Space

The state space represents the positions and velocities of all the drones in the problem, as well as the state of all the minearls in the domain.
The location and harvesting regions of the minearls are not part of the state, but are available through the non fluents in the problem.

| State                      | Type              |  Desc                                   |
|:---------------------------|:------------------|:----------------------------------------|
| pos_x(drone)               | Box(1, -np.inf, np.inf, float32)   | Position in x axis                      |
| vel_x(drone)               | Box(1, -np.inf, np.inf, float32)   |  Velocity in x axis                     |
| pos_y(drone)               | Box(1, -np.inf, np.inf, float32)   |  Position in y axis                     |
| vel_y(drone)               | Box(1, -np.inf, np.inf, float32)   |  Velocity in y axis                     |
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
- A. G. Barto, R. S. Sutton and C. W. Anderson, "Neuronlike adaptive elements that can solve difficult learning control problems," 
- in IEEE Transactions on Systems, Man, and Cybernetics, vol. SMC-13, no. 5, pp. 834-846.

<hr>
[Back to main page](index.md)

