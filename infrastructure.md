<p style="font-size:30px;text-align:center"><b>RDDL and the pyRDDLGym Infrastructure</b></p>

The problems in this year's competition will be described in the RDDL language.
RDDL is intended to compactly support the representation of a wide range of relational MDPs and POMDPs and support the efficient simulation of these domains. The domains will be simulated via autogenerating environment simulator and interacted via the standard [Gym](https://www.gymlibrary.dev/) interface. Simply put, the pyRDDLSim takes textual problem description in RDDL, and generates a gym environment without writing a single line of python code.


# Getting started with RDDL

RDDL is out there since 2010, with a JAVA simulator and excellent tutorial, explaining step by step with the help of a simple and illustrative example the power of RDDL and how to describe an MDP as an RDDL domain and instance. 

- [RDDL tutorial](https://sites.google.com/site/rddltutorial/)
- [JAVA RDDLSim](https://github.com/ssanner/rddlsim)

It is highly recommanded to read through the tutorial even without cloning the JAVA simulator to get the hanf of it. Note that in order to use pyRDDLGym (see next section) it is not required to fully understand RDDL, pyRDDLGym is fully gym compatible simulator, and can be treated as such, with the knowledge that the environments are not written in python but in RDDL.

The RDDL language guide which documents all the language components is also available here:
- [RDDL language guide](http://users.cecs.anu.edu.au/~ssanner/IPPC_2011/RDDL.pdf)

Please cite as

```
@unpublished{Sanner:RDDL,
      author = "Scott Sanner",
      title = "Relational Dynamic Influence Diagram Language (RDDL): Language Description",
      note = "http://users.cecs.anu.edu.au/~ssanner/IPPC_2011/RDDL.pdf",
      year = 2010}
```

# pyRDDLSim

pyRDDLSim is a generic autogeneration simulator from RDDL files to OpenAI Gym environments.

## Paper 
Coming soon!
<!-- Please see our paper describing the design decisions and implementation details behind pyRDDLGym. -->

## Status 
pyRDDLSim implements a subset of the capabilities of the full RDDL language, the things not included with the current distribution of pyRDDLSim is the following:
-  No enums.
-  leveling is available but not required anymore, pyRDDLSim can reason the dependencies and thus the level arguments of derived-fluents and interm-fluents can be omitted.
-  state-action-constrains is deprecated in favor of state-invariants and action-preconditions
-  action-preconditions are not checked during simulations and should be enforced by the cpfs directly. Only actions-preconditions of the form `action <= BOUND` and `action >= BOUND` are parsed for the benefit of gym spaces definitions.


## Getting started
The pyRDDLGym infrastructure is available for cloning: `https://github.com/ataitler/pyRDDLGym.git`

Read the [Readme page](https://github.com/ataitler/pyRDDLGym/README) for information on the framework contents, requirements, examples, and more.

## Basic usage

### Initializing Environments
Initializing environments is very easy in pyRDDLGym and can be done via: 
```python
from Env import RDDLEnv as RDDLEnv
myEnv = RDDLEnv.RDDLEnv(domain="domain.rddl", instance='instance.rddl')
```

### Interacting with the Environment
pyRDDLGym is build on Gym as so implements the classic “agent-environment loop”. 
The infrastructure comes with two simple agents:

1. **NoOpAgent** - which allows the environment to evolve according to the default behavior as specified in the RDDL file.
2. **RandomAgent** - which sends a rendom action according to the env.action_space and the maximum number of allowed concurrent actions as specified in the RDDL file.


Using a pre existing agent, or using of of your own is as simple as:
```python
from Policies.Agents import RandomAgent
agent = RandomAgent(action_space=myEnv.action_space, num_actions=myEnv.NumConcurrentActions)
```


Let’s see what a complete the agent-environment loop looks like in pyRDDLGym.
This example will run the instance `instance.rddl` of the problem specified in the file `domain.rddl`.
The loop will run for the amount of time steps specified in the environment's `horizon` field. If the env.render() function will be used we will also see a window pop up rendering the environment
```python
from Env import RDDLEnv as RDDLEnv
from Policies.Agents import RandomAgent

myEnv = RDDLEnv.RDDLEnv(domain='domain.rddl', instance='instance.rddl')
agent = RandomAgent(action_space=myEnv.action_space, num_actions=myEnv.NumConcurrentActions)

total_reward = 0
state = myEnv.reset()
for _ in range(myEnv.horizon):
      next_state, reward, done, info = myEnv.step(agent.sample_action())
      total_reward += reward
myEnv.close()
```

### Spaces

The state and action spaces of pyRDDLGym are standard `gym.spaces`, and inquireable througth the standard API: `env.state_space` and `env.action_space`.
State/action spaces are of type `gym.spaces.Dict`, where each key-value pair where the key name is the state/action and the value is the state/action current value or action to apply.

Thus, RDDL types are converted to `gym.spaces` with the appropriate bounds as specified in the RDDL `action-preconditions` and `state-invariants` fields.
The conversion is as following:
- real -> Box with bounds as specified in `action-preconditions`, or with `np.inf` and symetric bounds.
- int -> Discrete with bounds as specified in `action-preconditions`, or with `np.inf` and symetric bounds.
- bool -> Discrete(2)

There is no need in pyRDDLGym to specify the values of all the existing action in the RDDL domain description, only thus the agent wishes to assign non-default values, the infrastructure will construct the full action vector as necessery with the default action values according to the RDDL description.

Note: enum types are not supported by pyRDDLGym at this stage.

### Constants
RDDL allows for the constants of the problem instead of being hardcoded, to be specified and in the non-fluent block of the instance. Meaning every instance can have different constants, e.g., different bounds on action, different static object location, etc.

While these constants are not available through the state of the problem, it is possible to access them through gym (or directly through the RDDL description) with a dedicated API: `env.non_fluents`. The non_fluents property returns a python dictionary where the keys are the grounded non-fluents and the values are the appropriate values. 


### Visualization

pyRDDLGym visualization is just like regular Gym. Users can visualize the current state of the simulation by calling `env.render()`. The standard visualizer that comes out of the box with every pyRDDLGym domain is the TextViz. TextViz just render an image with textual description of the states and their current values.

Replacing the built is TextViz is simple as calling the environment method `env.set_visualizer(viz)` with `viz` as the desired visualization object.

In order to build custom visualiztions (for new user defined domains), one just need to inherit the class `Visualizer.StateViz.StateViz()` and return in the `visualizer.render()` method a PIL image for the gym to render to the screen.

### Custom user defined domains

Writing a new user defined domains is as easy as writing a few lines of text in a mathematical fashion!
All is required is to specify the lifted constants, variables (all are refered as fluents in RDDL), behavior/dynamic of the problem and generating an instance with the actual objects and initial state in RDDL - and pyRDDLGym will do the rest.

<hr>
[Back to main page](index.md)
