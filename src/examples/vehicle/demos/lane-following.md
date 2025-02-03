# Demo: Lane Following

## Introduction

This demo reproduces the lane following demo by executing each of the libraries in the pipeline.
There is no `ROS` involved, it is pure python.

This demo is designed to work with the map `loop_0`, which can be found in the `duckiematrix-examples` repository.
For this demo, using a different map might not produce the expected result, as the requested vehicle might not be present in the other map.


## Step 1: Build the demo

To build the demo, open a terminal and run the following command from the `duckiematrix-examples/vehicle/demos/lane_following` directory:

    dts devel build --pull


## Step 2: Run the Duckiematrix

To launch the Duckiematrix renderer on the map `loop_0`, open another terminal and run the following command from the `duckiematrix-examples/maps` directory:

    dts matrix run --standalone --map loop_0

```{note}
If you are running on MacOS you will see the Finder open and you should click on the Duckiematrix icon to start the renderer
```


## Step 3: Run the demo

To run the demo, once built, run the following command in the first terminal:

    dts devel run -X

You should see a `matplotlib` window pop up and the Duckiebot starting to move, as shown in the following video:

```{vimeo} 835872522
```
