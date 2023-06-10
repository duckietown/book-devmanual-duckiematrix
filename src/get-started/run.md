(run-duckiematrix)=
# Run the Duckiematrix

In this section, we will see how we can run the Duckiematrix.

The Duckiematrix is, by design, a distributed platform. This means that multiple
components are needed for the system to work as a whole. Luckily, `dts` can do
all this for us.


(run-duckiematrix-in-sandbox)=
## Run in a Sandbox

The easiest way to enter a session of the Duckiematrix is to run it in **Standalone**
and **Sandbox** modes. The **Standalone** mode makes sure all the necessary modules are
launched in the right order. The **Sandbox** mode loads one of the example maps that come
with the platform.

Let's run,

```shell
dts matrix run --standalone --sandbox
```

The command above should start a local engine and a local renderer.


(run-duckiematrix-with-remote-engine)=
## Run using a Remote Engine

The engine does not have to run on your local computer. In fact, it is quite boring to
run local engines, because you will be running around your beautifully simulated towns
all by yourself. Remote engines allow you to join virtual Duckietowns with your friends
and colleagues. We shall talk about all the nice things you can do on remote engines
later in the book.

If somebody asks you to join them on their remote virtual Duckietown, ask them for the
hostname or IP address of their engine and run the following,

```shell
dts matrix run --engine IP_OR_HOSTNAME
```

The command above should **only** start a local renderer which will connect to the
remote engine at the hostname/IP provided.
