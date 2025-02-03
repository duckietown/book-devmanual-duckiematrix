(connecting-virtual-duckietown-robots-matrix)=
# Connecting to the Duckiematrix

It is possible to connect a virtual Duckietown robot to a respective entity in the Duckiematrix.
This allows for the testing of the robot's full software stack in a photorealistic simulation, allowing for integration testing of developed ROS nodes or custom Docker images.

```{attention}
Make sure that the shell is using an `ente` profile.
```


## 1. Start the virtual robot

To start the virtual robot `VIRTUAL_ROBOT_NAME`, run:

    dts duckiebot virtual start VIRTUAL_ROBOT_NAME


## 2. Starting the Duckiematrix

In order to attach the virtual Duckietown robot to the Duckiematrix we need to know how to reach the latter.
To obtain the IP address of the Duckiematrix, you can start it with the `--verbose` flag:

    dts matrix run --standalone --sandbox --verbose

In this case, we are running the matrix in the `standalone` mode (both the engine and renderer) and using the `sandbox` map.
Once the Duckiematrix has started, there will be a list of different IP addresses where it is reachable and the respective networks it can be reached from.
Since the ROS containers on the Duckietown robot are connected to their own Docker network, we need to use the Duckiematrix IP address that is reachable from the local network, labeled `(local network only)`:

    INFO:duckiematrix:The Engine can be reached at any of these IP addresses:

        -  127.0.0.1         	(local machine only)
        -  192.168.1.20      	(local network only)
        -  172.17.0.1        	(local machine only)
        -  172.21.0.1        

In this case, we would pick the IP address `192.168.1.20`.
To run the engine on a different machine from the one your virtual Duckietown robot is on, consult the [](run-remote-engine) section.


## 3. Attaching the virtual Duckietown robot to the Duckiematrix

To attach a virtual Duckietown robot to a Duckiematrix entity, we need to know:

- `ENGINE_HOSTNAME`: the IP address/hostname where the Duckiematrix is reachable

- `VIRTUAL_ROBOT_NAME` : the name of the virtual Duckiematrix we want to attach

- `ENTITY_NAME` : The name of the Duckiematrix entity we want to attach to

To attach the virtual Duckietown robot `VIRTUAL_ROBOT_NAME` to the Duckiematrix entity `ENTITY_NAME`, run:

    dts matrix attach [-e ENGINE_HOSTNAME] VIRTUAL_ROBOT_NAME ENTITY_NAME

```{see-also}
For more information on the connection process between virtual Duckietown robots and Duckiematrix entities, consult the
[](ros-connector) section.
```


## 4. Connect to the virtual Duckietown robot

The virtual Duckietown robot will now behave in accordance with its physical equivalent (depending on the supported features, consult the [](driver-implementation-status) section).

To connect to `VIRTUAL_ROBOT_NAME` via `ssh`, run:

    ssh duckie@VIRTUAL_ROBOT_NAME

To control to `VIRTUAL_ROBOT_NAME` using a keyboard, run:

    dts duckiebot keyboard_control VIRTUAL_ROBOT_NAME

Try running a virtual lane following demo, as instructed in [Duckiebot lane following (LF) demo](demo-lane-following).
