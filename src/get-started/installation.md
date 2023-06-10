(install-duckiematrix)=
# Installation


As we found out in :ref:`Architecture`, for an instance of the Duckiematrix to work properly,
you need two components: an **engine** and a **renderer**.

(install-duckiematrix-engine)=
## Install the Engine

The Duckiematrix Engine comes as a Docker image called `duckietown/dt-duckiematrix`.
This image is automatically downloaded when needed, so you don't need to do anything for now.


(install-duckiematrix-renderer)=
## Install the Renderer

The renderer can be installed using `dts`.

```{note}
Make sure you have `dts` installed. 
You can install it by following the [official instructions](book-opmanual-duckiebot:laptop-setup-shell).
```

You can install the renderer using the command:

```bash
dts matrix install
```

This command should download the latest version of the renderer available from the internet
and unpack it into `~/.duckietown/duckiematrix/releases/`.
If you experience any issues with this command, please open an issue
[here](https://github.com/duckietown/duckietown-shell-commands/issues).
