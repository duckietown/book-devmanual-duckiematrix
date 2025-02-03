(world-links)=
# World Links

In the previous sections we saw how to run an instance of the Duckiematrix.
However, you may have noticed that the robots weren't doing much more than sitting and waiting.
This is because we did not tell the engine where to get robot commands from.
We can tell the engine to setup a communication channel with one of those robots and return to us *the other end of the line*, using `links`.


## What is a link?

```{figure} ../_images/get-started/world-links-1.jpg
:width: 100%
:name: fig:world-links

Example of world links between two agents and two robots
```

Links, or more properly *world links* (depicted in blue in {numref}`fig:world-links`), can be seen as communication channels between a robot on the matrix side and an entity on the world side, which could be either a (human) user or an algorithm.
For example, we could establish a link to a Duckiebot inside the environment to take control of it using a joystick from outside the engine, or attach an algorithm to it for autonomous driving, etc.

Links are bidirectional, and can carry sensory data from inside the engine out to the world, such as camera images or wheel encoder readings, or relay commands from the world to the
robot inside the engine.


## Establish a link

We can ask the engine to setup a `link` between an entity inside the Duckiematrix and a world entity by passing the argument `--link MATRIX WORLD` to the `dts matrix run` and
`dts matrix engine run` commands.
The value of `MATRIX` will be the key of the entity we want to connect to and `WORLD` will be a proxy name on the world side.

For example, if we launch the Duckiematrix in sandbox mode, we can see that the vehicle inside the environment is called `map_0/vehicle_0`.
That is its `MATRIX` key.
Let us now pick a proxy name for it, say `my_robot`, so that we can communicate with the robot from the world side.
In this case, run:

    dts matrix run --standalone --sandbox --link map_0/vehicle_0 my_robot

```{todo}
Add docs about connecting to a virtual robot or an agent
```
