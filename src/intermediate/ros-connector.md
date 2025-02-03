(ros-connector)=
# ROS Connector

The Duckiematrix comes with a [ROS](https://www.ros.org/) connector that allows for the connection of Duckietown robots to the Duckiematrix. 

Both physical and virtual Duckietown robots can be connected to the Duckiematrix using a ROS connector.
Physical robots connected to the Duckiematrix allow for hardware-in-the-loop simulation of agents, while virtual robots provide a fully simulated solution.

The intercommunication between ROS and the Duckiematrix happens at the level of the hardware drivers. 
In particular, _virtual_ versions of the drivers found in the [`dt-duckiebot-interface`](https://github.com/duckietown/dt-duckiebot-interface) repository are implemented using the [](python-sdk). 
This allows for virtual sensor (e.g., camera, time-of-flight, etc.) data to be bridged from the Duckiematrix to the ROS network (ROS messages).
Similarly, virtual actuator (e.g., motor, LED, etc.) drivers receive control commands from the ROS network and then relay these commands to the Duckiematrix engine.

{numref}`fig:ros-connector-hw-drivers-sim` shows the underlying architecture of hardware drivers for a Duckiebot connected to an instance of the Duckiematrix, while {numref}`fig:ros-connector-hw-drivers-real` shows the architecture of hardware drivers for a real-world Duckiebot (no Duckiematrix).

```{figure} ../_images/intermediate/block-ros-connector-hw-drivers-sim.png
:width: 100%
:name: fig:ros-connector-hw-drivers-sim

Architecture of hardware drivers for a Duckiebot connected
to a Duckiematrix.
```

```{figure} ../_images/intermediate/block-ros-connector-hw-drivers-real.png
:width: 100%
:name: fig:ros-connector-hw-drivers-real

Architecture of hardware drivers for a real-world Duckiebot (no Duckiematrix).
```


## Attach a Duckietown robot to a Duckiematrix entity

For a Duckietown robot to act and sense inside the Duckiematrix, it needs a proxy in the Duckiematrix (a Duckiematrix entity) to _attach_ to.
A robot outside the Duckiematrix is said to be _attached_ to a Duckiematrix entity when all of its sensors and actuators are linked to their virtual counterparts inside the Duckiematrix.

To attach a Duckietown robot to a Duckiematrix entity, run the following command, where `ROBOT` is the name of the robot and `ENTITY` is the name of the entity (e.g., `map_0/vehicle_0`):

    dts matrix attach [-e ENGINE_HOSTNAME] ROBOT ENTITY


### The Duckiematrix link description message

```{note}
This section is for advanced use only.
It allows us to trigger a connection programmatically instead of using `dts`.
You can skip this if using the command `dts matrix attach` is enough for your needs.
```

A Duckietown robot can connect to an Duckiematrix entity using the ROS message `duckietown_msgs/DuckiematrixLinkDescription`.
These messages have the following structure, where `matrix` is the name of the Duckiematrix instance (for when there are multiple instances), `uri` is usually a URL where the Duckiematrix engine can be reached and `entity` is the name of the entity:

```C
string matrix
string uri
string entity
```

Publishing an instance of this message on the ROS network of the Duckietown robot on the ROS topic `/VIRTUAL_ROBOT_NAME/duckiematrix/connect` will trigger the creation of a connection between every driver node and the Duckiematrix engine.
For convenience, an HTTP API endpoint is made available on the robot that will populate and publish this message for us.
Such an endpoint is available at `http://VIRTUAL_ROBOT_NAME.local/ros/duckiematrix/connect?matrix=...&uri=...&entity=...`.

````{tip}
An easy way to do this is by using the following command:
```shell
curl "http://VIRTUAL_ROBOT_NAME.local/ros/duckiematrix/connect?matrix=test&uri=172.16.2.37&entity=map_0/vehicle_0"
```
````
