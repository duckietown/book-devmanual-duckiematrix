(run-remote-engine)=
# Launch a Remote Engine

The Duckiematrix is, by design, a distributed platform, meaning that you can scatter pieces around across an arbitrarily large geographical region, as long as they are able to talk to each other over the network.
When you are not running in standalone mode, you need to tell the renderers where to reach the engine by providing either a hostname or an IP address, as described in the [](run-duckiematrix-with-remote-engine) section.

Once the remote engine is running, remote (or local) renderers can join in.
Depending on where the renderers are (logically) located within the network with respect to the engine, your setup will need to meet different requirements.

We can distinguish between three different engine reachability domains:

- **local machine** only

- **local network** only

- **global network** (internet)

To start an instance of the engine in sandbox mode, run:

    dts matrix engine run --sandbox

```{note}
We are using sandbox mode to keep the example simple.
You can pass your own map if you wish.
```

Once the engine is ready to accept connections from renderers, a list of IP addresses that the engine can be reached at will be shown:

    ...
    INFO:duckiematrix:The Engine can be reached at any of these IP addresses:

    -  127.0.0.1         	(local machine only)
    -  192.168.0.17      	(local network only)
    -  192.168.128.1     	(local network only)
    -  172.17.0.1        	(local machine only)


(run-engine-local-machine)=
## Local machine only

This is the easiest case, and normally occurs when we are running our system in standalone mode.
Both the engine and renderers run on the same machine, and will communicate over the [loopback](https://en.wikipedia.org/wiki/Loopback) network.
There are no special network requirements for this case, as the engine and renderers will reside on the same machine and use a network that is local to the machine.


(run-engine-local-network)=
## Local network only

This is a more common case, and allows for the scattering of renderers around a local network.
This is very useful when we want to speed up the simulation process by distributing the rendering tasks among several machines.
The only requirement, in this case, is that all of the renderers can reach the network in which the engine resides.


(run-engine-public-network)=
## Global network (internet)

This is a more rare case, as it is quite unlikely that you have a machine with a public IP address, as the vast majority of machines are connected to the internet through a local NAT.
Similarly to the local network configuration above, we now have the requirement that all of the renderers can reach the internet.
Moreover, the engine needs access to a public IP.

```{warning}
Exposing a Duckiematrix engine to the internet is not safe.
The Duckiematrix is not designed to account for malicious attacks.
Public engines need to be properly protected against attacks.
Use it at your own risk.
```


(run-engine-behind-nat)=
## Use behind a NAT

Note that, the renderers are the ones initiating the connection with the engine, not the other way around.
Therefore, it is important that the renderers are able to reach the engine when the connection hasn't been established yet, meaning that it is okay for the renderers to be behind a [NAT](https://en.wikipedia.org/wiki/Network_address_translation) but not the engine.
