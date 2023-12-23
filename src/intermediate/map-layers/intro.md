(map-layers)=
# Map Layers

The Duckiematrix uses the map format v2 as representation for the world. This format breaks the map into 
a set of YAML files called layers, each one adding a bit of information about the world.

For example, a vehicle in the scene has:
- its position and orientation described in the `frames.yaml` layer;
- its model and color described in the `vehicles.yaml` layer;
- its camera's intrinsics parameters described in the `camera.yaml` layer;
- etc...