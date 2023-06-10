(intro-capabilities)=
# Capabilities

The Duckiematrix was born to serve as the base rendering engine for 3D applications
in Duckietown.

- Embedded capabilities to simulate sensors like cameras, wheel encoders,
  time-of-flight lidars, IMUs, etc make it perfect for simulating robots in Duckietown;

- A proprietary, high-performance, distributed rendering orchestrator allows the simulation
  of arbitrarily large fleets of robots by distributing the rendering tasks across
  multiple GPUs/computers over the network;

- A naturally distributed architecture with a central configurator node removes any needs
  for network configurations;

- Over-the-network rendering makes it easy to develop video games, education-on-demand portals,
  virtual gatherings platforms, live broadcasting of public (or private) events like competitions
  or research experiments, all in a fully navigable 3D environment;

- Environment representation based on the
  [multi-layer world definition format](https://ethidsc.atlassian.net/wiki/spaces/DS/pages/448593943/Design+Document+Duckieworld+format)
  provides human-readable map representations that are easily extendable.

- The `Scriptable Map` feature allows the definition of custom behaviors using Python scripts
  embedded alongside the map definition.

- Executable locally without the need for persistent internet connections.
