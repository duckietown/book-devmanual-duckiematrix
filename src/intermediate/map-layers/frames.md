(map-layer-frames)=
# Map Layer - Frames

The `frames` layer is stored in the file `frames.yaml` and contains information about the skeleton of the 
world. Every solid object or movable part of an object has its 3D pose defined in the `frames` layer.

An example of frames layer is the following:

```yaml
version: 1.0
frames:
  map_0:
    relative_to: ~
    pose:
      x: 0
      y: 0
      z: 0
      roll: 0
      pitch: 0
      yaw: 0
  map_0/street_light_0:
      relative_to: ~
      pose:
          x: 0.6
          y: 0.6
          z: 0
          roll: 0
          pitch: 0
          yaw: 3.1415
```

In the example above, we see how a hierarchy of two objects and their pose is described. The object `map_0` 
is positioned at the origin, while an object `map_0/street_light_0` is positioned at `60cm` along both the 
`x` and `y` axis, `0cm` elevation, `180deg` rotation about the `Z` axis.

A pseudo-schema of the frames layer is the following,

```yaml
version: Str
frames: Dict[Str, Frame]
```

The `frames` object in the schema above is a mapping between object `keys` and their `Frame`.

## Object keys are not interpretable

While some keys might suggest what types of objects they refer to, e.g., `map_0/street_light_0` likely refers 
to a street lamp inside a city map, no assumptions can be made on the nature of the objects simply
by looking at their keys. In fact, any alphanumeric string is a valid key, and, though terribly misleading, 
it would not be illegal for the key `map_0/street_light_0` to refer to a tree, or a building.


## Frame object

A `Frame` object has the following pseudo-schema,

```yaml
relative_to: Optional[Str]
pose:
    x: Float
    y: Float
    z: Float
    roll: Float
    pitch: Float
    yaw: Float
```

where, `pose.x`, `pose.y`, ..., `pose.yaw` describe the 3D pose of the object. More on the `relative_to`
field in section [](map-layer-frames-relative-to) below.


## Hierarchy of objects

A frame's key has two functions. It serves as unique identifier for the object and encodes the hierarchical 
structure of the world. For example, in the `frames` layer above, the key `map_0/street_light_0` indicates
that the object `street_light_0` is a child of the object `map_0`, so if `map_0` moves, then `street_light_0`
will rigidly move together with its parent.

```{note}
The existence of on object's ancestors is not enforced. This means that a frames layer in which a frame with 
key `a/b/c` is defined but neither `a` nor `a/b` are is still a valid layer. In this case, dummy objects `a` 
and `a/b` will be created (so that `b` is a children of `a`) and their pose set to coincide with the origin
of the world.
```

(map-layer-frames-relative-to)=
## Relative to

While the path-like structure of keys encode the hierarchical structure of the world, sometimes we might want 
to define the pose of an object with respect to another object while keeping the two objects
on different branches of the hierarchy. In this case, the field `relative_to` can be used.

For example, in the `frames` layer

```yaml
version: 1.0
frames:
  map_0:
    relative_to: ~
    pose:
      x: 0
      y: 0
      z: 0
      roll: 0
      pitch: 0
      yaw: 0
  map_0/street_light_0:
      relative_to: ~
      pose:
          x: 0.6
          y: 0.6
          z: 0
          roll: 0
          pitch: 0
          yaw: 3.1415
  map_0/vehicle_0:
      relative_to: map_0/street_light_0
      pose:
          x: 1.0
          y: 0
          z: 0
          roll: 0
          pitch: 0
          yaw: 0
```

we wanted to express the desire to place the vehicle `map_0/vehicle_0` at a distance of `1m` (along `X`) 
from the the street light `map_0/street_light_0`.
In this case, relying solely on the hierarchical structure of the key would have forced a constraint between 
a vehicle and a street lamp that very likely did not exist.

```{note}
While we could have achieved the same result even without the field `relative_to` simply by using the pose of 
the frame `map_0/street_light_0` with respect to `map_0` to compute the pose of the vehicle, this would have
required a-priori compute and loss of information as well as a loss of readability and editability of the 
scenario.
```
