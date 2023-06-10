# I/O: LED

## Introduction

This demo is designed to work properly with the map `loop_0` you find
in the `duckiematrix-examples` repository.
Using this demo with a different map might not produce the
expected result as the requested vehicle might not be present
in the new map.

## Step 1: Build the demo

Run the following command from inside the `duckiematrix-examples/vehicle/io/led` directory to build the demo.

```shell
dts devel build
```

## Step 2: Run the Duckiematrix

Run the following command from inside the directory `maps/` you can
find at the root of the `duckiematrix-examples` repository to launch the Duckiematrix on the
map `loop_0`.

```shell
dts matrix run --standalone --map ./loop_0
```

You should see a Duckiematrix renderer pop up.

## Step 3: Run the demo

Run the following command from inside this directory to run the demo.

```shell
dts devel run -X
```

You should see the Duckiebot's LEDs changing in the Duckiematrix.
