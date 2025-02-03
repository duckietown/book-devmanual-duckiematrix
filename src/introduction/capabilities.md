(intro-capabilities)=
# Capabilities

The Duckiematrix was built to serve as the base rendering engine for 3D applications in Duckietown.
It is capabile of:

- Simulating sensors, such as cameras, wheel encoders, time-of-flight lidars, IMUs, etc.

- Simulating arbitrarily large fleets of robots, by distributing the rendering tasks across multiple GPUs/computers over the network, thanks to Duckietown's proprietary high-performance distributed rendering orchestrator

- Working without the need for network configuration, due to its naturally distributed architecture and central configurator node

- Over-the-network rendering, making it easy to develop video games, education-on-demand portals, virtual gathering platforms, live broadcasting of public or private events, such as competitions and research experiments, within a fully navigable 3D environment

- Representing environments based on the [multi-layer world definition format](https://ethidsc.atlassian.net/wiki/spaces/DS/pages/448593943/Design+Document+Duckieworld+format), providing human-readable map representations that are easily extendable

- Accepting custom behaviors, using Python scripts embedded alongside the map definition, thanks to the `Scriptable Map` feature

- Local executability, removing the need for a persistent internet connection
