# Demo: Lane Following


## Introduction

This demo reproduces the lane following demo by executing each of the libraries in the pipeline. There is no ROS involved, it is pure python.

To find the demo clone the [duckiematrix-examples](https://github.com/duckietown/duckiematrix-examples) repository and navigate to the `duckiematrix-examples/vehicle/demos/lane_following` directory. 

This demo is designed to work properly with the map `loop_0` that  you will also find
in the `duckiematrix-examples/maps` directory.
Using this demo with a vehicle with different camera/kinematics
parameters from those in `map_0/vehicle_0` in the map `loop_0` will affect
the behavior.


## Step 1: Build the demo

From the demo directory, run the following command to build the demo.

```shell
dts devel build --pull
```


## Step 2: Run the Duckiematrix

Run the following command, also from inside the demo directory:

```shell
dts matrix run --standalone --map ../../../maps/loop_0
```

You should see a Duckiematrix renderer pop up.

## Step 3: Run the demo

Run the following command from inside this directory to run the demo (you will need a new shell for this).

```shell
dts devel run -X
```

You should see a matplotlib window pop up and the vehicle inside the
Duckiematrix start moving.

```{vimeo} 835872522

Lane following running in the Duckiematrix
```