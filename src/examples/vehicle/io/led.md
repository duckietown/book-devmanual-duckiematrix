# I/O: LED

## Introduction

This demo is designed to work with the map `loop_0`, which can be found in the `duckiematrix-examples` repository.
For this demo, using a different map might not produce the expected result, as the requested vehicle might not be present in the other map.


## Step 1: Build the demo

To build the demo, open a terminal and run the following command from the `duckiematrix-examples/vehicle/io/led` directory:

    dts devel build --pull


## Step 2: Run the Duckiematrix

To launch the Duckiematrix renderer on the map `loop_0`, open another terminal and run the following command from the `duckiematrix-examples/maps` directory:

    dts matrix run --standalone --map loop_0


## Step 3: Run the demo

To run the demo, once built, run the following command in the first terminal:

    dts devel run

You should see the Duckiebot's LEDs changing, as shown in the following video:

```{vimeo} 835872551
```
