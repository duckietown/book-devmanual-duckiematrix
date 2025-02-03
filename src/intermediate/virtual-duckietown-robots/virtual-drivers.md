# Virtual Drivers

Virtual drivers allow for the communication between a Duckietown robot's ROS stack and an entity in the Duckiematrix.


(driver-implementation-status)=
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
  - The wrong speed is achieved

* - Display
  - Broken
  - 
```


## Virtual Drivers I/O Diagram

{numref}`fig:virtual-drivers-exchanged-objects` shows what type of data each of the drivers receives or sends to the Duckiematrix.
The interfaces are developed using the [](python-sdk).

```{figure} ../../_images/intermediate/virtual-drivers.png
:name: fig:virtual-drivers-exchanged-objects

Data types exchanged with the Duckiematrix by the virtual drivers.
```
