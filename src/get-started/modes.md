(modes)=
# Modes

A Duckiematrix network can run in two modes:

- **realtime** mode;
- **simulation** (or **gym**) mode;


(mode-realtime)=
## Realtime Mode

```{figure} ../_images/get-started/mode-realtime-1.jpg
:width: 100%
:name: fig:mode-realtime

Sequence diagram of a simple Duckiematrix network running in `realtime` mode
```
    

In **realtime** mode, the Matrix side and the World side works `asynchronously` with respect
to one another. Agents on the World side can send inputs to the Matrix as fast as they want
and the Matrix will consume them as fast as it can. If the Matrix does not manage to keep up
with the agents, some commands will be dropped and never reach the Matrix.

Similarly, sensors in the renderers will (try to) produce data at the sensor's frequency,
regardless of how much data the agents can process. In fact, neither side will care whether
there is somebody at all listening on the other side.
Figure {numref}`fig:mode-realtime` shows an example of a Duckiematrix network in which
an agent and a renderer produce outputs asynchronously from each other.

This is exactly what happens with real robots, so it is a very interesting mode to have.
While this is the mode that most closely resembles the real behavior of a robot and an agent,
it evolves with dynamics that are non-deterministic. This means that experiments run in
realtime mode are not reproducible. For this reason, the scientific community prefers systems
that run in synchronous mode.

The job of the Engine in this case is an easy one, which is that of running the physics engine
on the commands from the World side whenever they are available, and bridge data from the Matrix
side over to the World side.


(mode-gym)=
## Simulation (gym) Mode

```{figure} ../_images/get-started/mode-gym-1.jpg
:width: 100%
:name: fig:mode-gym

Sequence diagram of a simple Duckiematrix network running in `simulation` mode
```
    

The simulation mode, also known as **gym** mode, is `synchronous`.
Starting from the Matrix side, robots will produce their observations (sensors readings),
which will be collected by the Engine and sent as a whole to the World side.
The renderers will be paused until the World side has produced all its outputs.
When this happens, the Engine will collect them and run the physics engine which act on those
commands. An updated state of the world is sent to the renderers, which will start producing
another batch of observations.
Figure {numref}`fig:mode-gym` shows an example of a Duckiematrix network in which
an agent and a renderer are kept in sync by the engine.

The strenuous job performed by the Engine in this case guarantees that all the renderers
start a batch of rendering/sensing only once all the robots in the scene have received a
command from the World side. Overall performances in simulation mode are greatly reduced
compared to the realtime mode due to the synchronicity of the events.
