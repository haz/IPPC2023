# Movie Generation

## Intro

pyRDDLGym comes with a usefull functionality for generating movies from episodes of interaction with the environement.
The generated movies are animated GIFs that can be used for illustration of the policy effectiveness. 
The functionality is triggered directly from the environment object, but a movie generation object should be supplied for that.

## Movie Generation
The object which generates the movies is
```
pyRDDLGym.Visualzier.MovieGenerator
```
This object is instantiated with a directory to save the temporary frames and movies, name for the movies, and maximum number of frames of each movie.
There are several other optional arguments that can be specified, please see the pyRDDLGym documentation for more information.

## How to Generate Movies
The movie generation object is passed on to the environement through the environement `set_visualizer` method:
```python
env.set_visualizer(vizObject, MovieGenObject, movie_per_episode)
```
Only the VizObject is mendatory when invoking the `set_visualizer` method, the MovieGen object and movie_per_episode flag are optional.
Note that if one desires to generate a movie from the default visualizer, the TextViz object can be used.
The `movie_per_episode` toggles between two modes, if true, a movie will be generated for every episode upon invoking the `reset()` method.
If false then only a single movie will be generated when the `close()` method of the environment will be invoked.
