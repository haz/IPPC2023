<p style="font-size:25px;text-align:left"><b>Cart Pole Control</b></p>

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
| GRAVITY      | float32          |  Force of gravity acting down                       |
| FORCE_MAG    | float32          |  Force applied to the side of the cart              |
| CART_MASS    | float32          |  Mass of the cart                                   |
| POLE_MASS    | float32          |  Mass of the pole                                   |
| POLE_LEN     | float32          |  Half of the pole length                            |
| TIME_STEP    | float32          |  Seconds between state updates                      |
| POS_LIMIT    | float32          |  Limit of cart position                             |
| ANG_LIMIT    | float32          |  Limit of pole angle                                |

All of these can be read from the RDDLEnv interface and from the RDDL files.

## Action Space

There is a single action taking {0,1} values, indicating if the cart should be pushed to the left or to the right.

| Action               | Type             |  Desc                                                  |
|:---------------------|:-----------------|:-------------------------------------------------------|
| force_side           | Discrete(2)      |  whether to apply force to left, right side or none    |

If force_side is 0 then the cart is pushed to the left with FORCE_MAG force \
If force_side is 1 then the cart is pushed to the right with FORCE_MAG force 

**Note**: The velocity that is reduced or increased by the applied force is not fixed and it depends on the angle the pole is pointing. The center of gravity of the pole varies the amount of energy needed to move the cart underneath it

- FORCE_MAG is available from the RDDLEnv interface and in the RDDL domain and instance.

## State Space

The state space represents the positions and velocities of all the drones in the problem, as well as the state of all the minearls in the domain.
The location and harvesting regions of the minearls are not part of the state, but are available through the non fluents in the problem.

| State             | Type                                   |  Desc                         |
|:------------------|:---------------------------------------|:------------------------------|
| pos               | Box(1, -POS_LIMIT, POS_LIMIT, float32) |  Cart position                |
| ang_pos           | Box(1, -ANG_LIMIT, ANG_LIMIT, float32) |  Pole angle                   |
| vel               | Box(1, -np.inf, np.inf, float32)       |  Cart velocity                |
| ang_vel           | Box(1, -np.inf, np.inf, float32)       |  Pole angular velocity        |

**Note**: The bounds above denote the possible values for the state space of each element. upon violation of one of these values the episode will continuo without change (the state will be frozen, and reward zero), for the remaining of th episode.

- POS_LIMIT and ANG_LIMIT are available from the RDDLEnv interface and in the RDDL domain and instance.
- 
## Rewards
Since the goal is to keep the pole upright for as long as possible, a reward of +1 for every step taken, including the termination step, is allotted.


## References
- A. G. Barto, R. S. Sutton and C. W. Anderson, "Neuronlike adaptive elements that can solve difficult learning control problems," 
- in IEEE Transactions on Systems, Man, and Cybernetics, vol. SMC-13, no. 5, pp. 834-846.

<hr>
[Back to main page](index.md)

