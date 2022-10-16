
<p style="font-size:25px;text-align:left"><b>Power Unit Commitmentn</b></p>

<div style="width:100%;text-align:center;">
  <a href="images/Rpowergen_static.png">
    <img src="images/powergen_static.png" height="190" width="190" />
  </a>
</div>

|       |      |
|:------------------|:------------|
| Import folder     | Power_gen  |
| Action space      | Dict        |
| State space       | Dict        |


## Description

A number of power producers cooperate to meet daily demand that fluctuates according to the maximum temperature on a given day. A cost is incurred for every unit of power produced and income is received for every unit consumed by the demand.
There is a large penalty for failing to meet demand on a given day and there are per-power plant penalties for deviating from the previous day’s production at each plant – some plants must pay higher operating costs for changes in production. Power generation is in integer units, consumption is real, and time steps are assumed to span 24 hours.

## Action Space

The actions are the current amount of power each plant is required to produce.

| Action               | type             |  Desc                          |
|:---------------------|:-----------------|:-------------------------------|
| curProd(plant)       | Discrete(PROD_UNITS_MIN, PROD_UNITS_MAX)  |  current production command to each plant |


## State Space

The state space represents the temerature and the previous production of each of the plants in the problem.

| State                      | type              |  Desc                                   |
|:---------------------------|:------------------|:----------------------------------------|
| temperature                | Box(1, float32)   | Current temperature                     |
| prevProd(plant)            | Discrete(-inf, inf)   |  previous power produced per plant      |


## Rewards

The reward function is defined as 

cost of supply per plant, demand income, demand exceeds supply penalty, steady-state penalties

## References

- http://en.wikipedia.org/wiki/Power_system_simulation 

<hr>
[Back to main page](index.md)

