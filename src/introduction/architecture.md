(intro-architecture)=
# Architecture

For an instance of the Duckiematrix to work properly, two components are required:

- An **engine**

- A **renderer**

```{figure} ../_images/introduction/block-architecture-1.jpg
:width: 100%
:align: center

Block diagram of a simple Duckiematrix network
```

For the sake of ease, we will be focusing on the example of a single engine serving a
single renderer. This is probably the most common use case, but definitely not the only
one. In fact, while you always want to have a single engine per instance of a map, you
can have as many renderers as you want connected to the same engine. This has a lot of
benefits, which are discussed later in this book.

For the remainder of this book, we will use the words "renderers" even to refer to cases
in which a single renderer is present.
The engine always considers a list of renderers, so the simple case in which only a single renderer is present is the case in which the engine has a list of one element, nothing more.

We use the term **Duckiematrix network** to indicate a set of renderers connected
to an engine, including the engine itself.


(intro-the-engine)=
## The engine

The **engine** is the component that is responsible for reading the map from disk, together with scripts and assets that come with it, and sending them all together, in a single
compressed package called "the context", to all the renderers connected.
The context is all a renderer needs to initialize the map. It is just enough for the renderers to place the correct objects in their initial locations.


(intro-the-renderer)=
## The renderer

The **renderer** is the component that is responsible for rendering the content of the context and simulating sensors.
While the engine runs in a terminal, the renderer has a GUI component, which requires a screen.
However, this is not a strict limitation, as it is possible to run a renderer using off-screen rendering, where a memory buffer serves as a virtual screen. This is discussed later in this book.


(intro-communication)=
## Communication

The engine and renderers talk to each other over the network, whose infrastructure is built using the [ZeroMQ](https://zeromq.org/) framework.
Messages are implemented using a custom flavor of the open-source [CBOR (RFC 8949 Concise Binary Object Representation)](https://cbor.io/>).


## How it works

You can think of renderers as very boring video games, in which a virtual environment is shown, but nothing happens in it. Nothing moves, not even birds in the sky.
Everything is frozen in time, until the engine unfreezes them for a short period of time, called a time step.
The job of the engine is to process time steps as fast as possible.

For each time step, the engine has a lot of processing to do, such as computing the physics of the objects in the scene or regulating when sensors should fire and lights should turn on/off.
Changes from one time step to the next are represented as `diffs` (differences) in the content of the map layers that describe the scene.

At every time step, the new `diffs` are sent to the renderers, which in turn apply them to their scenes (effectively moving objects around, turning lights on/off, etc.). 
Do this fast enough, and you will see that the "video games" you see in the renderers don't look so boring anymore.
Birds will actually fly, cars will drive, wheels will spin, broken lights will flicker, just the way they are intended to. You can think of this process as a (possibly giant) distributed [stop-motion movie](https://www.youtube.com/watch?v=_ppedXZHhE0).

The simplicity of the architecture is its greatest feature, allowing one to leverage the power of video-game-grade 3D renderers while keeping full control of the scene and physics simulation.
