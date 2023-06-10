(run-remote-engine)=
# Launch a Remote Engine

The Duckiematrix is, by design, a distributed platform.
This means that you scatter pieces around across an arbitrarily large geographical
region, as long as they are able to talk to each other over the network.
When you are not running in Standalone mode, you need to tell you renderers where to
reach the engine by providing either a hostname or an IP address, as described in
[](run-duckiematrix-with-remote-engine).

Once you remote engine is running, remote (or local) renderers can join in.
Depending on where your renderers will be (logically) located within the network
with respect to the engine, your setup will need to meet different requirements.

We can distinguish between three different engine reachability domains:

- **local machine** only
- **local network** only
- **global network** (internet)

You can run an instance of the engine in **Sandbox** mode using the command,

```shell
dts matrix engine run --sandbox
```

```{note}
We are using the **Sandbox** mode to keep the example simple. You can pass your
own map if you wish.
```

Once the engine is ready to accept connections from renderers, a list of IP
addresses that the engine can be reached at will be shown. For example, a classical
output will look like the following,

```shell
...
INFO:duckiematrix:The Engine can be reached at any of these IP addresses:

 -  127.0.0.1         	(local machine only)
 -  192.168.0.17      	(local network only)
 -  192.168.128.1     	(local network only)
 -  172.17.0.1        	(local machine only)
```


(run-engine-local-machine)=
## Local Machine only

This is the easiest case, and it normally happens when we are running our system in
Standalone mode. Both the engine and the renderers run on the same physical computer, and
they will communicate over the so called [loopback](https://en.wikipedia.org/wiki/Loopback)
network.

There are no special network requirements for this case, as the engine and the renderers
will reside on the same machine and they will use a network that is local to the device.


(run-engine-local-network)=
## Local Network only

This is a more common case, and it allows us to scatter renderers around a local network.
This is very useful when we want to speed up the simulation process by distributing the
rendering tasks among several computers and GPUs.

The only requirement in this case is that all your renderers can reach the network in
which the engine resides.


(run-engine-public-network)=
## Global Network (Internet)

This is a more rare case, as it is quite unlikely that you have a computer with a public
IP address. The vast majority of computers are connected to the internet through a local
NAT.

Similarly to the local network configuration above, we now have the requirement that all
your renderers can reach the internet. Moreover, your engine needs access to a public IP.

```{warning}
Exposing a Duckiematrix engine to the internet is not safe. The Duckiematrix is not
designed to account for malicious attacks. Public engines need to be properly protected
against attacks. Use it at your own risk.
```


(run-engine-behind-nat)=
## Use behind a NAT

Remember, the renderers are those initiating the connection towards the engine, not the
other way around. This is why it is important for the renderers to be able to reach the
engine when the connection hasn't been established yet.
For this reason, it is ok for the renderers to be behind a
[NAT](https://en.wikipedia.org/wiki/Network_address_translation)
but not for the engine.
