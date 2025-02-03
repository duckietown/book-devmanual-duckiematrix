(virtual-duckiebots-dts-commands)=
# DTS Commands

You can interact with virtual Duckietown robots using `dts`.
To update your `dts` commands to the latest available versions, run:

    dts update

The following subcommands are used to interact with the virtual Duckietown robots and perform operations that are specific to the physical robots and do not have a counterpart in the virtual world. 
To run a specific `<subcommand>`, run:

    dts duckiebot virtual <subcommand>


## `connect`

To connect to the virtual robot `VIRTUAL_ROBOT_NAME`, run:

    dts duckiebot virtual connect VIRTUAL_ROBOT_NAME


## `create`

To create the virtual robot `VIRTUAL_ROBOT_NAME`, run the following command, where `TYPE` is the type of virtual robot to create and `CONFIGURATION` is the configuration of the virtual robot:

    dts duckiebot virtual create --type TYPE --configuration CONFIGURATION VIRTUAL_ROBOT_NAME


## `destroy`

To destroy the virtual robot `VIRTUAL_ROBOT_NAME` and remove all of its Docker images from the local machine, run:

    dts duckiebot virtual destroy VIRTUAL_ROBOT_NAME


## `list`

To list the existing virtual robots and their statuses, run:

    dts duckiebot virtual list


## `restart`

To restart the virtual robot `VIRTUAL_ROBOT_NAME`, run:

    dts duckiebot virtual restart VIRTUAL_ROBOT_NAME


## `start`

To start the virtual robot `VIRTUAL_ROBOT_NAME`, run:

    dts duckiebot virtual start VIRTUAL_ROBOT_NAME


## `stop`

To shut down the virtual robot `VIRTUAL_ROBOT_NAME`, run:

    dts duckiebot virtual stop VIRTUAL_ROBOT_NAME
