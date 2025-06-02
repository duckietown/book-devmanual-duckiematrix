(run-duckiematrix)=
# Run the Duckiematrix

In this section, we will learn how to run the Duckiematrix.

The Duckiematrix is, by design, a distributed platform, meaning that multiple components are needed for the system to work as a whole.
Luckily, `dts` can do all of this for us.


(run-duckiematrix-in-sandbox)=
## Run in a sandbox

The easiest way to enter a session of the Duckiematrix is to run it in **standalone** or **sandbox** mode.
**Standalone** mode ensures that all of the necessary modules are launched in the right order.
**Sandbox** mode loads one of the example maps that comes with the platform.
To start a local engine and renderer, run:

    dts matrix run --standalone --sandbox --tutorial


(run-duckiematrix-with-remote-engine)=
## Run using a remote engine

The engine does not have to run on your local computer.
In fact, it is quite boring to run local engines, because you will be running around your beautifully simulated towns all by yourself.
Remote engines allow you to join virtual Duckietowns with your friends and colleagues.
The capabilites of remote engines will be discussed later in this book.

If somebody asks you to join them on their remote virtual Duckietown, ask them for the hostname or IP address of their engine.
To start a local renderer and connect to the remote engine at the hostname or IP provided, run:

    dts matrix run --engine IP_OR_HOSTNAME
