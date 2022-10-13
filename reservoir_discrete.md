The reservoir domain represents a network of water tanks interconnected in a DAG structure.
Each tank state is the tank actual water level, which is bounded by zero from bellow and the maximum height of the tank from above. 
Any excess of water beyond the top of the tank is spilled out and lost. The inflow to the tank is the inflow from other tanks, and stochastic rainfall.
The outflow is the stochastic evaporation of water, spill of overflowing water and active release of water to the network.

The incoming water from other tanks is a cumulative sum of all flows to the tank. The outflow is controlled by the release, 
which defines an absolute amount leaving the tank, which then dispensed equally among the connected tanks.
The goal is to keep all the tanks water levels between the minimum and maximum bounds.
