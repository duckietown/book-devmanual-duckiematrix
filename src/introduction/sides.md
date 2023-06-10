(intro-matrix-vs-world)=
# Matrix vs World

In a running instance of Duckiematrix, we distinguish between two sides:

- **matrix** side;
- **world** side;


```{figure} ../_images/introduction/block-architecture-2.jpg
:width: 100%
:align: center

Block diagram of a simple Duckiematrix network
```


(intro-matrix-side)=
## Matrix Side

The **matrix** side is the one containing all the renderers. When we say that
something happens on the matrix side, we mean that it is something that is computed,
or an event that has occurred, in one or many renderers.

(intro-world-side)=
## World Side

The **world** side is where we (human) users and robots reside. Note that we are not
making a distinction between virtual and physical robots here. The line is a little
blurry here, but let us address it right away.
Robots, intended as computing entities, whether virtual or physical, always reside
on the world side. Their sensors and actuators though, reside on the matrix side.

Any world entity (e.g., user, algorithm, robot, etc.) that interacts with the engine
from the world side is called **agent**.


## The Engine has no side

Sitting between the world and the matrix side, the engine does not belong to any of the two.
In a Duckiematrix network, the engine is responsible, among other things,
for bridging data between the world side and the matrix side, and back.
It controls the data flow between the sides and makes sure that everybody is getting what
they need from the other side.
