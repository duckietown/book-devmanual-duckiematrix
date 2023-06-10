# Getting started developing in Duckiematrix

## Setup environment

1. Clone the needed repositories:

    ```bash
    git clone git@github.com:duckietown/dt-duckiematrix.git
    git clone git@github.com:duckietown/duckiematrix.git
    git clone git@github.com:duckietown/duckiematrix-examples.git
    ```

## Structure of the software

The file entities are defined in `packages/duckiematrix_engine/entites`. To define a new entity, inheriting i.e. from `DifferentialDriveVehicleEntityAbs` we can create a new file e.g. `DynamicsVehicleEntity.py`

## Workflow

It is useful to have an overview of the development workflow:

1. Make changes to source code in `packages/duckiematrix_engine` (repo `dt-duckiematrix`)
2. Build the new engine for Duckiematrix
3. Run it

## Building the project

In this step we need to build the engine with the changes we made, in order to test them.
This step will build a new image of the duckiematrix that will be automatically pushed to
the Docker registry and used for running the duckiematrix locally.
To build the Docker image run:

```bash
dts devel build
```

## Running the project

This image will be used by default by the Duckiematrix to run. As an example if you want to
test a change locally in the `sandbox` map you can execute:

```bash
dts matrix run --sandbox --standalone
```
