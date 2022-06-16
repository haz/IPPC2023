## Welcome to the 2023 International Probabilistic Planning Competition

The International Probabilistic Planning Competition is organized in the context of the International Conference on Planning and Scheduling (ICAPS). It empirically evaluates state-of-the-art planning systems on a number of benchmark problems. The goals of the IPC are to promote planning research, highlight challenges in the planning community and provide new and interesting problems as benchmarks for future research.

Since 2004, probabilistic tracks have been part of the IPC under different names (as the International Probabilistic Planning competition or as part of the uncertainty tracks). After 2004, 2006, 2008, 2011, 2014, and 2018, the 7th IPPC will be held in 2023 and conclude together with ICAPS, in June 2023, in 
Prague (Czech Republic). This time it is organized by Ayal Taitler and Scott Sanner.


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
Coming soon!

## Domains

<details>
  <summary style="font-size:18px; font-weight:bold">Multi-tank reservoir control</summary>
  
  The reservoir domain represents a network of water tanks interconnected in a DAG structure.
  Each tank state is the tank actual water level, which is bounded by zero from bellow and the maximum height of the tank from above. Any excess of water beyond the 
  top of the tank is spilled out and lost. The inflow to the tank is the inflow from other tanks, and stochastic rainfall. The outflow is the stochastic evaporation of 
  water, spill of overflowing water and active release of water to the network.

  The incoming water from other tanks is a cumulative sum of all flows to the tank. The outflow is controlled by the release, which defines an absolute amount leaving
  the tank, which then dispensed equally among the connected tanks. The goal is to keep all the tanks water levels between the minimum and maximum bounds.

</details>

<hr>

<details>
  <summary style="font-size:18px; font-weight:bold">Multi-rover Mars science mission</summary>


    Multi-agent path finding (MAPF) problem, where agents starts from a some initial position, and should harvast as many minerals as possible. Each mineral is
    locatied randomly at the instatiation of the problem, and has different value. Agent dynamics in each axis is a second order integrator i.e., linear rate of change
    
    for each agent the state vector is the position and velocity, and the action is the acceleration. The full state vector is the stacking of all agents' states, and 
    similarly for the actions. The reward is the total rewards collected from harvesting the mineral, minus the power consumption usued throughout the process.

</details>

<hr>

**Multi-zone HVAC control**

<pre style="font-size:18px; font-weight:bold"> sdfsdfsdf </pre>

The Heating Ventilation and Air-Conditioning (HVAC) domain deals with a problem of a zone temperature being regulated by a heat source, and a fan.
<hr>


More information coming soon!

## Results
Coming soon!

## Organizers
- [Ayal Taitler](https://sites.google.com/view/ataitler/home) (University of Toronto)
- [Scott Sanner](https://www.mie.utoronto.ca/faculty_staff/sanner/) (University of Toronto)

Contact us: [ippc2023-rddl@googlegroups.com](ippc2023-rddl@googlegroups.com)
