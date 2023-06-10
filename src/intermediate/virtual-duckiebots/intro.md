# Virtual Duckiebots

Virtual Duckiebots allow us to run the full Duckiebot software stack on your local machine
in its own Docker environment. This allows us to fully simulate any aspect of a Duckiebot,
enabling integration tests.

To interact with the virtual duckiebots you can use the `dts duckiebot virtual` subcommands,
detailed in [](virtual-duckiebots-dts-commands).

Once the virtual duckiebot is running they behave just like a real Duckiebot, so you can use the 
same commands of the duckietown shell that you would use with a real robot to interact with them.

## Limitations
| Features | Real Duckiebots    | Virtual Duckiebots |
| :------- | ------------------ | -----------------: |
| GPU      | Supported on `DB21+` | Not tested (could be supported if host supports it) |