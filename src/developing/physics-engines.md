# Physics Engines

The physics engines take care of updating the pose of the entities they are associated with.
They should implement a `.step` method that takes in a `delta_t` value and provides an updated pose.
Currently, the following physics engines are implemented:

| Entity                    | Physics Engine | Description                                                          |
| ------------------------- | -------------- | -------------------------------------------------------------------- |
| `DifferentialDriveEntity` | Kinematic      | Updates poses based on velocity and time                             |
| `DynamicsVehicleEntity`   | Dynamic        | Simulates realistic physical interactions                            |
| `QuadCopterEntity`        | rotorpy[^1]    | Simulates the dynamics of a quadrotor, including aerodynamic effects |

[^1]: [rotorpy](https://github.com/spencerfolk/rotorpy), a quadrotor dynamics simulator.
