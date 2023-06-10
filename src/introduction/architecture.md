(intro-architecture)=
# Architecture

For an instance of the Duckiematrix to work properly, you need two components:

- An **engine**;
- A **renderer**;


```{figure} ../_images/introduction/block-architecture-1.jpg
:width: 100%
:align: center

Block diagram of a simple Duckiematrix network
```

For the sake of ease, we will be focusing on the example of a single engine serving a
single renderer. This is probably the most common use case, but definitely not the only
one. In fact, while you always want to have a single engine per instance of a map, you
can have as many renderers as you want connected to the same engine. This has a lot of
benefits, and we shall talk about all of them later in this book.

For the remainder of this book, we will use the words "renderers" even to refer to cases
in which a single renderer is present. The engine always considers a list of renderers, so
the simple case in which only a single renderer is present is the case in which the engine
has a list of one element, nothing more.

We use the term **Duckiematrix network** to indicate a set of renderers connected
to an engine, including the engine itself.


(intro-the-engine)=
## The Engine

The **engine** is the component that is responsible for reading the map from disk,
together with scripts and assets that come with it and send all together, in a single
compressed package, that we call "the context", to all the renderers connected.
The context is all a renderer needs to initialize the map. It is just enough for the
renderers to place the correct objects in their initial locations.


(intro-the-renderer)=
## The Renderer

The **renderer** is the component that is responsible for rendering the content of the
context and simulating robots' sensors. While the engine runs in a terminal, the renderer
has a GUI component, so it has to run on a computer with a screen attached.
This is not a strict limitation. In fact, it is possible to run a renderer using
off-screen rendering, where a memory buffer serves as a virtual screen. We shall talk
about this later in the book.


(intro-communication)=
## Communication

The engine and the renderers talk to each other using the network. Messages are implemented
using a custom flavor of the open-source 
[CBOR (RFC 8949 Concise Binary Object Representation)](https://cbor.io/>).
The network infrastructure is built using the [ZeroMQ](https://zeromq.org/) framework.


## How it works

You can think of renderers as very boring video games, in which a virtual environment is shown,
but nothing happens in it. Nothing moves, not even birds in the sky. Everything is frozen in
time, until the engine unfreezes them for a short period periof of time, called time step.
The job of the engine is that of processing time steps as fast as possible.

For each time step, the engine has a lot of processing to do, for example it computes the physics
of the objects in the scene, it regulates when sensors should fire or lights turn on (or off).
Changes from one time step to the next are represented as `diffs` (differences) in the content of
the map layers that describe the scene.

At every time step, the new `diffs` are sent to the renderers, which in turn apply them to their
scenes (effectively moving objects around, turning lights on/off, etc.). Do this fast enough,
and you will see that the "video games" you see in the renderers don't look so boring anymore.
Birds will actually fly, cars will drive, wheels will spin, broken lights will flicker, just the
way they are intended to. You can think of this process as a (possibly giant) distributed
[stop-motion movie](https://www.youtube.com/watch?v=_ppedXZHhE0).

The simplicity of the architecture is its greatest feature. The reasoning behind this is that
of leveraging the power of video-game-grade 3D renderers (while stripping out everything that
depends on time, like physics) while keeping full control of the scene and the physics simulation.
