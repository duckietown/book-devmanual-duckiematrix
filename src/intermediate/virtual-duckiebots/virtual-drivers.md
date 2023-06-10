# Virtual Drivers

Virtual drivers allow communication between the Duckiebot
ROS stack and the entity in the Duckiematrix.
## Implementation status
```{list-table}
:header-rows: 1
:name: virtual-drivers-status-table

* - Driver
  - Working
  - Limitations

* - Camera
  - Yes
  - 

* - Time of Flight
  - No
  -

* - IMU
  - No
  - 

* - LED
  - Yes
  - 

* - Encoders
  - No
  -

* - Wheels
  - Partially
  - The wrong speed is achieved.

* - Display
  - Broken
  - 
```

## Virtual Drivers I/O Diagram

In the following diagram we show what type of data each of the drivers receives or sends to the Duckiematrix:

```{figure} ../../_images/intermediate/virtual-drivers.png
:name: virtual-drivers-exchanged-objects

Data types exchanged with the Duckiematrix by the virtual drivers.
```

The interfaces are developed using the Python SDK, detailed in [](python-sdk).