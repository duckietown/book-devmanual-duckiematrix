(connecting-virtual-duckiebots-matrix)=
# Connecting to the Duckiematrix

It is possible to connect a virtual Duckiebot to a respective Duckiebot entity in the Duckiematrix.
This allows to test in a photorealistic simulation the entire stack of the Duckiebot, allowing for integration
testing of developed ROS nodes or custom Docker images.

```{attention}
Make sure that the shell is set to the `ente` version with:

    dts --set-version ente

```

## 1. Start the virtual robot

The first step is to start the virtual robot by executing:

    dts duckiebot virtual start ENTITY_NAME

You can find a list of all the virtual duckiebots with the command

    dts duckiebot virtual list

## 2. Starting the Duckiematrix

In order to attach the virtual Duckiebot to the Duckiematrix we need to know how to reach the latter. To
obtain the IP address of the Duckiematrix you can start it with the `--verbose` flag:

    dts matrix run --standalone --sandbox --verbose

In this case we are running the matrix in the `standalone` mode (both engine and renderer) and using the `sandbox` map.
Once the Duckiematrix has started there will be a list of different IP addresses where it is reachable and the respective networks it can be reached from.
Since the ROS containers on the Duckiebot are connected to their own Docker network we need to use the Duckiematrix IP address that is reachable from the local network, labeled `(local network only)`:

```bash
INFO:duckiematrix:The Engine can be reached at any of these IP addresses:

	 -  127.0.0.1         	(local machine only)
	 -  192.168.1.20      	(local network only)
	 -  172.17.0.1        	(local machine only)
	 -  172.21.0.1        
```

In this case we would pick the IP address `192.168.1.20`. If you want to run an engine in a different machine than the one your virtual duckiebot will be
running on look at [](run-remote-engine).

## 3. Attaching the virtual duckiebot to the matrix

To attach the virtual duckiebot to a matrix entity we need to know:

- `ENGINE_HOSTNAME`: the IP address/hostname where the Duckiematrix is reachable at.
- `VIRTUAL_ROBOT_NAME` : the name of the virtual Duckiebot we want to attach
- `ENTITY_NAME` : The entity of the Duckiematrix we want to attach to.

Then we can execute:

    dts matrix attach [-e ENGINE_HOSTNAME] VIRTUAL_ROBOT_NAME ENTITY_NAME

taking care of replacing the parameters with the correct values.

```{note}
You can find more details on the connections process between the virtual Duckiebots and the Duckiematrix in the
[](ros-connector) section.
```

## 4. Connect to the virtual Duckiebot

The virtual Duckiebot now will behave just as a real one would (depending on the supported features, see [](driver-implementation-status) ).
For example you can connect to it through ssh as:

```bash
ssh duckie@VIRTUAL_ROBOT_NAME
```

or control it with a Joystick using `dts duckiebot keyboard_control VIRTUAL_ROBOT_NAME`.

Try running a virtual lane following by following the instructions in [Duckiebot lane following (LF) demo](demo-lane-following)!