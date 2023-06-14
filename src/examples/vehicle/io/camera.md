# I/O: Camera

## Introduction

This demo is designed to work properly with the map `loop_0` you find
in the `duckiematrix-examples` repository.
Using this demo with a different map might not produce the
expected result as the requested vehicle might not be present
in the new map.

## Step 1: Build the demo

Run the following command from inside this directory to build the demo.

```shell
dts devel build --pull
```

## Step 2: Run the Duckiematrix

Run the following command from inside the directory `duckiematrix-examples/maps/` you can
find at the root of the examples' repository to launch the Duckiematrix on the
map `loop_0`.

```shell
dts matrix run --standalone --map ./loop_0
```

You should see a Duckiematrix renderer pop up.

## Step 3: Run the demo

Run the following command from inside this directory to run the demo. The `-X` flag enables windows rendering, to show the camera images.

```shell
dts devel run -X
```

You should see a matplotlib window pop up rendering the image captured
by the vehicle's camera in the Duckiematrix.

```{image} ../../../_images/examples/camera_io.png
:width: 600px
```