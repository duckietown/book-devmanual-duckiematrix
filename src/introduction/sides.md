(intro-matrix-vs-world)=
# Matrix vs World

In a running instance of Duckiematrix, we distinguish between two sides:

- The **matrix** side

- The **world** side

```{figure} ../_images/introduction/block-architecture-2.jpg
:width: 100%
:align: center

Block diagram of a simple Duckiematrix network
```


(intro-matrix-side)=
## The matrix side

The **matrix** side contains all of the renderers.
When we say that something happens on the matrix side, we mean that it is something that is computed, or an event that has occurred, in one or many renderers.


(intro-world-side)=
## The world side

The **world** side is where we (human) users and robots reside.
Note that we are not making a distinction between virtual and physical robots here.
Robots, intended as computing entities, whether virtual or physical, always reside on the world side. Their sensors and actuators though, reside on the matrix side.

Any world entity (e.g., user, algorithm, robot, etc.) that interacts with the engine from the world side is called **agent**.


## The Engine has no side

Sitting between the world side and matrix side, the engine does not belong to either.
In a Duckiematrix network, the engine is responsible for, among other things, bridging data between the two sides, ensuring that everyone gets what they need from the other side.
