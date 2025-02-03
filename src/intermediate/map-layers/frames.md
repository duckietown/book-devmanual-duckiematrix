(map-layer-frames)=
# Map Layer - Frames

The `frames` layer is stored in the `frames.yaml` file and contains information about the skeleton of the world, where every solid object or movable part of an object has its 3D pose defined in the `frames` layer.

The following is from a `frames.yaml` file, where the `map_0` object is positioned at the origin and the `map_0/street_light_0` object is positioned `60cm` along the `x` and `y` axes, and `0cm` along the `z` axis, with a rotation of `180deg` about the `z` axis:

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

A pseudo-schema of the frames layer is as follows, where the `frames` object is a mapping between object `keys` and their `Frame`:

```yaml
version: Str
frames: Dict[Str, Frame]
```


## Object keys are not interpretable

While certain keys suggest the types of objects they refer to (e.g., `map_0/street_light_0` likely refers to a street lamp inside a city map), no assumptions can be made about the nature of the objects simply by looking at their keys.
In fact, any alphanumeric string is a valid key and, though terribly misleading, the key `map_0/street_light_0` could refer to a tree, building, etc.


## Frame object

A `Frame` object has the following pseudo-schema, where `pose.x`, `pose.y`, `pose.z`, `pose.roll`, `pose.pitch` and `pose.yaw` describe the 3D pose of the object, and more information on the `relative_to` field can be found in the [](map-layer-frames-relative-to) section:

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


## Hierarchy of objects

A frame's key has two functions, it serves as a unique identifier for the object and encodes the hierarchical structure of the world.
For example, in the `frames` layer above, the `map_0/street_light_0` key indicates that the `street_light_0` object is a child of the `map_0` object.
Therefore, if `map_0` moves, then `street_light_0` will rigidly move together with its parent.

```{note}
The existence of an object's ancestors is not enforced.
This means that a frame's layer in which a frame with key `a/b/c` is defined but neither `a` nor `a/b` are, is still a valid layer.
In this case, dummy objects `a` and `a/b` will be created (so that `b` is a child of `a`) and their poses will be set to coincide with the origin of the world.
```


(map-layer-frames-relative-to)=
## Relative to

While the path-like structure of keys encode the hierarchical structure of the world, sometimes we might want to define the pose of an object with respect to another object while keeping the two objects on different branches of the hierarchy.
In this case, the `relative_to` field can be used.
For example, in the following `frames` layer, we wanted to position the `map_0/vehicle_0` object `1m` from the `map_0/street_light_0` object along the `x` axis:

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

In this case, relying solely on the hierarchical structure of the key would have forced a constraint between two objects that may not have existed.

```{note}
While we could have achieved the same result without the `relative_to` field, by using the pose of the `map_0/street_light_0` object with respect to the `map_0` object, this would have required a-priori compute and a loss of information, as well as a loss of readability and editability of the scenario.
```
