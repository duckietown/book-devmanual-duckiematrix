# Virtual Duckietown Robots

Virtual Duckietown robots allow for a Duckietown robot's full software stack to be run on a local machine in its own Docker environment, allowing for the full simulation of any aspect of a Duckietown robot, enabling integration tests.

To interact with virtual Duckietown robots, use the `dts duckiebot virtual` subcommands, as described in the [](virtual-duckiebots-dts-commands) section.
Once a virtual Duckietown robot is running, it will behave in accordance with its physical equivalent, including how it responds to `dts` commands.

## Limitations

| Features | Physical Duckietown robots | Virtual Duckietown robots                           |
| -------- | -------------------------- | --------------------------------------------------- |
| GPU      | Supported on the `DB21+`   | Not tested (could be supported if host supports it) |
