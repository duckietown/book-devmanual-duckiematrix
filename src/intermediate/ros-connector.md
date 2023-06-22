(ros-connector)=
# ROS Connector

The Duckiematrix comes with a [ROS](https://www.ros.org/) connector that allows us to connect 
Duckiebots to the Duckiematrix. 

Both physical and virtual Duckiebots can be connected to the Duckiematrix using a ROS connector.
Physical Duckiebots connected to the Duckiematrix allow for hardware-in-the-loop simulation of
agents, while virtual Duckiebots provide a fully simulated solution.

The intercommunication between ROS and the Duckiematrix happens at the level of the hardware drivers. 
In particular, a _virtual_ version of all the drivers in the 
[`dt-duckiebot-interface`](https://github.com/duckietown/dt-duckiebot-interface) 
repository is implemented using the Duckiematrix [](python-sdk). 
These allow for virtual sensors (e.g., camera, time-of-flight, etc.) 
data to be bridged from the duckiematrix to the ROS network (ROS messages). 
Similarly, virtual actuators' drivers (e.g., motors, leds, etc.) receive control commands from the ROS 
network and relay them to the Duckiematrix engine.

The following diagram shows the underlying architecture of hardware drivers for a Duckiebot connected
to an instance of the Duckiematrix ({numref}`fig:ros-connector-hw-drivers-sim`).
For comparison, {numref}`fig:ros-connector-hw-drivers-real` shows the architecture of hardware
drivers for a real-world Duckiebot (no Duckiematrix).


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


## Attach a Duckiebot to the Duckiematrix

For a Duckiebot to act and sense inside the Duckiematrix, it needs a proxy in the virtual world
(a virtual Duckiebot) to _attach_ to. A Duckiebot outside the Duckiematrix is said to be
_attached_ to the Duckiematrix when all its sensors and actuators are linked to their virtual
counterparts inside the Duckiematrix.

We can use the following command to attach a Duckiebot to a running Duckiematrix,

```shell
dts matrix attach [-e ENGINE_HOSTNAME] VIRTUAL_ROBOT_NAME ENTITY_NAME
```

where `VIRTUAL_ROBOT_NAME` is the name of the Duckiebot outside the Duckiematrix and `ENTITY_NAME` is the
name of the virtual entity inside the Duckiematrix we want to connect to, for example, `map_0/vehicle_0`.


### The Duckiematrix Link Description message

```{note}
This section is for advanced use only. It allows us to trigger a connection programmatically instead of
using dts.
You can skip this if using the command `dts matrix attach` is enough for your needs.
```

The drivers of a Duckiebot can be asked to connect to a virtual sensor (or actuator) on a running
instance of a Duckiematrix using the ROS message `duckietown_msgs/DuckiematrixLinkDescription`.
Such message has the following structure,

```C
string matrix
string uri
string entity
```

where, `matrix` is the name of the Duckiematrix (not important when working with a single instance
of the Duckiematrix), `uri` is usually a URL at which the Duckiematrix engine can be reached,
and `entity` is the name of the virtual Duckiebot inside the Duckiematrix map that we want to
attach our Duckiebot to.

Publishing an instance of this message on the ROS network of the Duckiebot on the ROS topic 
`/VIRTUAL_ROBOT_NAME/duckiematrix/connect` will trigger the creation of a connection between every driver
node and the Duckiematrix engine.

For convenience, an HTTP API endpoint is made available on the Duckiebot that will populate and
publish this message for us. Such endpoint is available at the URL 

`http://VIRTUAL_ROBOT_NAME.local/ros/duckiematrix/connect?matrix=...&uri=...&entity=...`.

```{tip}
An easy way to do this is by using the `curl` command, e.g. :

  curl "http://VIRTUAL_ROBOT_NAME.local/ros/duckiematrix/connect?matrix=test&uri=172.16.2.37&entity=map_0/vehicle_0"
```

