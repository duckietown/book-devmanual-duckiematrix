(map-layers)=
# Map Layers

The Duckiematrix uses the v2 map format to represent the world, which breaks the map up into a set of YAML files called layers, each adding information about the world.

For example, a Duckietown robot in the scene has its:

- position and orientation described in the `frames.yaml` layer

- model and color described in the `vehicles.yaml` layer

- camera's intrinsic parameters described in the `camera.yaml` layer
