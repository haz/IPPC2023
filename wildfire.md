<p style="font-size:25px;text-align:left"><b>Fire Fighting</b></p>


<div style="width:100%;text-align:center;">
  <a href="images/wildfire_image.gif">
    <img src="images/wildfire_image.gif" height="190" width="190" />
  </a>
</div>

|       |      |
|:------------------|:------------|
| Example name      | Wildfire    |
| Action space      | Dict        |
| State space       | Dict        |


## Description
Imagine that you are an emergency manager tasked to control a wildfire, as depicted in the animation on the right, and ultimately keep it away from important target locations, such as schools or residential houses. Consider that each cell on the map can either be burning (flame), out-of-fuel (gray), or neither (green) and you have the ability to both cut-out fuel from a non-target cell (causing it to be out-of-fuel and preventing it from igniting in the future) and put-out the fire occupying a burning cell. Cells are more likely to ignite as the number of their burning neighbouring cells increases

| Constant                 | Type             |  Desc                                               |
|:-------------------------|:-----------------|:----------------------------------------------------|
| COST-CUTOUT              | float32          |  Cost to cut-out fuel from a cell    |
| COST-PUTOUT              | float32          |  Cost to put-out a fire from a cell  |
| PENALTY-TARGET-BURN      | float32          |  Penalty for each target cell that is burning       |
| PENALTY-NONTARGET-BURN   | float32          |  Penalty for each non-target cell that is burning   |
| NEIGHBOR(x-pos, y-pos, x-pos, y-pos)   | bool          |  Topology of the cells                   |
| TARGET(x-pos, y-pos)     | bool          |  High value cells that should be protected from fire   |

All of these can be read from the RDDLEnv interface and from the RDDL files.


## Action Space

| Action               | Type            |  Desc                               |
|:--------------------|:-----------------|:------------------------------------|
| put-out(x-pos, y-pos)  | Discrete(2)   |  actions to put-out out the fire    |
| cut-out(x-pos, y-pos)  | Discrete(2)   |  cut-out out the fuel               |

All of these can be read from the RDDLEnv interface and from the RDDL files.


## State Space

| State                      | Type              |  Desc                                   |
|:---------------------------|:------------------|:----------------------------------------|
| burning(x-pos, y-pos)      | Discrete(2)       | cell currently on fire                   |
| out-of-fuel(x-pos, y-pos)  | Discrete(2)       |  cell does not have fuel to burn (i.e., cut-out or already burned)     |

All of these can be read from the RDDLEnv interface and from the RDDL files.


## Rewards


## References
- [Wildfire example](https://github.com/ataitler/pyRDDLGym/tree/main/pyRDDLGym/Examples/Wildfire)

<hr>
[Back to main page](index.md)




