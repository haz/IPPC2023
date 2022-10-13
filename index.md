<p style="font-size:30px;text-align:center"><b>Welcome to the 2023 International</b></p>
<p style="font-size:30px;text-align:center"><b>Probabilistic Planning Competition</b></p>

The International Probabilistic Planning Competition is organized in the context of the International Conference on Planning and Scheduling (ICAPS). It empirically evaluates state-of-the-art planning systems on a number of benchmark problems. The goals of the IPC are to promote planning research, highlight challenges in the planning community and provide new and interesting problems as benchmarks for future research.

Since 2004, probabilistic tracks have been part of the IPC under different names (as the International Probabilistic Planning competition or as part of the uncertainty tracks). After 2004, 2006, 2008, 2011, 2014, and 2018, the 7th IPPC will be held in 2023 and conclude together with ICAPS, in June 2023, in 
Prague (Czech Republic). This time it is organized by Ayal Taitler and Scott Sanner.

[Infrastructure](/infrastructure.md)

## Calls
Coming soon!

## Preliminary Schedule


| Event                                         | Date             |
|:----------------------------------------------|:-----------------|
| Expression of interest                        | June, 2022       |
| Infrastructure release with sample domains    | July, 2022       |
| Call for domains and praticipants             | August, 2022     |
| Final domains announcement                    | November, 2022   |
| Competitors registration                      | December, 2022   |
| Planner abstract dubmission                   | March, 2023      |
| Contest run                                   | April, 2023      |
| Results announced                             | June, 2023       |



## Tracks
Coming soon!

## Registration
Coming soon!

## Setup

This year's competition will be using the generic pyRDDLGym - an autogeneration tool for gym environments from RDDL textual description.

<img src="images/RDDLGym.jpg" alt="RDDLGym diagram">

More information about the infrastructure, how to use it and how to add user defined domains can be found in this short
[Infrastructure guide](/infrastructure.md).


## Domains

**Multi-tank reservoir control**

The reservoir domain represents a network of water tanks interconnected in a DAG structure.
  Each tank state is the tank actual water level, which is bounded by zero from bellow and the maximum height of the tank from above. Any excess of water beyond the 
  top of the tank is spilled out and lost. The inflow to the tank is the inflow from other tanks, and stochastic rainfall. The outflow is the stochastic evaporation of 
  water, spill of overflowing water and active release of water to the network.

  The incoming water from other tanks is a cumulative sum of all flows to the tank. The outflow is controlled by the release, which defines an absolute amount leaving
  the tank, which then dispensed equally among the connected tanks. The goal is to keep all the tanks water levels between the minimum and maximum bounds.

<hr>

**Multi-rover Mars science mission**

Multi-agent path finding (MAPF) problem, where agents starts from a some initial position, and should harvast as many minerals as possible. Each mineral is
locatied randomly at the instatiation of the problem, and has different value. Agent dynamics in each axis is a second order integrator i.e., linear rate of change
    
for each agent the state vector is the position and velocity, and the action is the acceleration. The full state vector is the stacking of all agents' states, and 
similarly for the actions. The reward is the total rewards collected from harvesting the mineral, minus the power consumption usued throughout the process.

<hr>

**Multi-zone HVAC control**

The Heating Ventilation and Air-Conditioning (HVAC) domain deals with a problem of a zone temperature being regulated by a heat source, and a fan.
An outer fan inserts new air into the system in a constant predefined rate. Zone fans are in-charge of pulling air out of the zones, some of that air is ventilated outside, and some is used for circulations. Heaters are in-charge of heating/cooling air to a desired temperature, which in controlled by means of heat transfer.
The heaters heat combination of outside and circulated air, for the heaters to heat the combined air to the desired temperature a heat quantity, which is correlated to the needed energy is used. Thus, the controlled variables in the problem are the power or the heat used to heat the air by the heaters, and the fan speeds or Variable Air Volume (VAV) being circulated by the zone fans. The states of the problem are the zones' temperatures, and the output air temperatures of the heaters.

The goal is to minimize the amount of energy used to operate the system - heating and venting, and to minimize the discomfort levels in the zones, defined as being outside of a parameterized comfort range.

<hr>

**Power Unit Commitment**

A number of power producers cooperate to meet daily demand that fluctuates according to the maximum temperature on a given day. 
A cost is incurred for every unit of power produced and income is received for every unit consumed by the demand.  
There is a large penalty for failing to meet demand on a given day and there are per-power plant penalties for deviating from the previous day's production at each plant -- some plants must pay higher operating costs for changes in production.
Power generation is in integer units, consumption is real, and time steps are assumed to span 24 hours.

<hr>

More information coming soon!


## Organizers
- [Ayal Taitler](https://sites.google.com/view/ataitler/home) (University of Toronto)
- [Scott Sanner](https://www.mie.utoronto.ca/faculty_staff/sanner/) (University of Toronto)

Contact us: [ippc2023-rddl@googlegroups.com](ippc2023-rddl@googlegroups.com)
