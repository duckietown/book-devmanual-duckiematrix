# Getting Started Developing in the Duckiematrix

## Setup environment

Clone the required repositories:

    git clone git@github.com:duckietown/dt-duckiematrix.git
    git clone git@github.com:duckietown/duckiematrix.git
    git clone git@github.com:duckietown/duckiematrix-examples.git


## Structure of the software

The file entities are defined in `packages/duckiematrix_engine/entites`.
To define a new entity inheriting from `DifferentialDriveVehicleEntityAbs`, for example, create a new file, such as `DynamicsVehicleEntity.py`.


## Workflow

It is useful to have an overview of the development workflow:

1. Make changes to the source code in `packages/duckiematrix_engine` (the `dt-duckiematrix` repository)

2. Build the new engine for the Duckiematrix

3. Run it


## Building the project

To test any changes made, the engine needs to be built, incorporating those changes.
This step will build a new image of the Duckiematrix that will be automatically pushed to the Docker registry and used for running the Duckiematrix locally.
To build the Docker image, run:

    dts devel build


## Running the project

This image will be used by default.
To test a change locally in the `sandbox` map, run:

    dts matrix run --sandbox --standalone
