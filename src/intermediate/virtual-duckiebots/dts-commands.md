(virtual-duckiebots-dts-commands)=
# DTS commands

You can interact with the virtual Duckiebots using the duckietown-shell. Always make sure to have the latest version
of the shell commands by running `dts update`.

The following sub-commands are used to interact with the virtual Duckiebots and perform operations that are specific to the real
Duckiebots and do not have a counterpart in the virtual world. 

You can run a specific `<subcommand>` by running `dts duckiebot virtual <subcommand>`. For each subcommand you can
use the flag `-h/--help` to have further details on its usage.

## `restart`

    dts duckiebot virtual restart <virtual_robot_name>

Allows us to restart the robot `virtual_robot_name`. 
This is the recommended way to reboot the virtual robot.

## `stop`

    dts duckiebot virtual stop <virtual_robot_name>

Allows us to shut down the robot `virtual_robot_name`. 
This is the recommended way to shut down the virtual robot.

## `destroy`

    dts duckiebot virtual destroy <virtual_robot_name>

Allows us to destroy the virtual robot `virtual_robot_name` and remove all its Docker images from the local machine.

## `create`

    dts duckiebot virtual create <virtual_robot_name>

This command will start the procedure to create a virtual duckiebot image, just like you would do when
flashing the SD card of a real Duckiebot.
The options you can provide are:

- `-t`/`--type` to specify the type of virtual robot to create
- `-c`/`--configuration` to provide Duckiebot configuration file

## `list`

    dts duckiebot virtual list

Will list all the existing virtual duckiebots and their status.

## `connect`

    dts duckiebot virtual connect

Allows for the connection of a real duckiebot to a virtual one.

## `start`

    dts duckiebot virtual start `virtual_robot_name`

Will start the virtual robot `virtual_robot_name` if it was stopped.