# Camera Calibration

## Extrinsics

## Introduction

In this tutorial we will see how to perform camera calibration
of a Duckiebot inside the Duckiematrix.
In this case, we are performing the extrinsic calibration.

This example is designed to work properly with the map `loop_0` you find
in this repository.
Using this demo with a vehicle with different intrinsics camera
parameters from those in `map_0/vehicle_0` in `loop_0` will affect
the result.

## Step 1: Build the demo

Run the following commands from the directory `duckiematrix-examples/vehicle/calibration/camera/extrinsics`.
To build the demo, run:

```shell
dts devel build
```

## Step 2: Run the Duckiematrix

Open another terminal and run the following command from inside the directory `duckiematrix-examples/maps/`

```shell
dts matrix run --standalone --map ./loop_0
```

This will launch the Duckiematrix renderer on the map `loop_0`.

## Step 3: Run the demo

Run the following command from inside this directory to run the demo.

```shell
dts devel run -X
```

You should see a matplotlib window pop up showing the image recorded by the
robot's front camera.

## Step 4: Go to the laboratory

In the Duckiematrix window:

- select Mayor's View (top-right corner of the window);
- walk to the vehicle you see on the road;
- press <kbd>E</kbd> to hop on the vehicle;
- use the keys <kbd>W</kbd>, <kbd>A</kbd>, <kbd>S</kbd>, <kbd>D</kbd> to drive;
- drive to the laboratory's driveway, then press <kbd>F</kbd> to enter the building;
- select the Extrinsics Calibration tool (bottom-center of the window);

## Step 5: Wait for a good detection

```{figure} ../../../_images/examples/extrinsic_calibration.png

Detected corners in the calibration procedure
```

The matplotlib window opened during Step 3 will show the corners detected 
on the patterned board. Once you see a clear and correct detection of all corners, 
press <kbd>ENTER</kbd> in the terminal from Step 3 and the estimated homography
will be printed to screen.
