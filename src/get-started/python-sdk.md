(python-sdk)=
# Python SDK

The Duckiematrix comes with a Python SDK that allows for the development of both environment and agent behaviors.

```{todo}
Explain the SDK here
```


# Entities I/O

## Sensors

Sensors have a common API, comprised of several methods that can be called:

- To create a connection with a sensor on an entity, use the `.start()` method

- To open the connection with the sensor, use the `.attach()` method, which has a `callback` parameter that can be a `Callable` that processes the messages. Several callbacks can be added using this method

- To remove a callback from the sensor stream, use the `.detach()` method, providing it with a `callback` parameter

- To close the connection with the sensor, use the `.release()` method

- To obtain a message from a sensor, use the `.capture()` method, which accepts two parameters:

    - `block : bool = False`, to optionally make the driver wait (up to a timeout) to receive the frame before moving on

    - `timeout: float = None`, to specify the timeout for the `block` parameter


### Camera

The camera API allows us to obtain images from the Duckiematrix.
The obtained images are JPEG-encoded by default.
The API is available to any entity of type `CameraEnabledRobot`.

To obtain a frame from the camera, use the `.capture()` method:

```python
msg : CameraFrame = CameraEnabledRobot.capture(block=True, timeout=1)
```

The obtained message is of type `CameraFrame` and has the following fields:

```python
CameraFrame

format: str   # Image format
width: int    # Width of the image in pixels
height: int   # Height of the image in pixels
frame: bytes  # Raw content of the image
```


### Time-of-flight 

The time-of-flight sensors provide the ranges measured by the virtual entity, which can be obtained using the `.capture()` method, where the messages obtained will be of type `TimeOfFlightRange`:

```python
TimeOfFlightRange

range: float  # Time-of-flight range
```


### Encoders

The encoders provide the ticks measured by the virtual entity, which can be obtained using the `.capture()` method, where the message obtained will be of type `WheelEncoderTicks`:

```python
WheelEncoderTicks

ticks: int  # Encoder ticks
```


## Actuators

Actuators allow us to interact with the Duckiematrix environment.
Duckiebots have wheel motors to control the two wheels and LEDs to visually communicate with humans and other Duckiebots.


### Wheels driver

```{todo}
To update once the wheels communication protocol has been defined.
```

### LEDs

The LED configuration reflects that of Duckiebots, allowing for the control of 5 LEDs, indexed from `0` to `4`.
In this case, the object that allows for the manipulation of the LEDs is of type `Lights`, which contains each LED as an `LED` object.
Each `LED` object, `i`, can be retrieved by calling `<Lights>.light<i>`. 

Each `LED` object has a `color` property with 3 color channels (red `r`, green `g` and blue `b`), which can each be set to a different value in the range `[0-255]`.
To display any changes, use the `.atomic()` context, as it will automatically commit any changes to the engine:

```python
with self.robot.lights.atomic():
    for light in self.robot.lights:
        light.color.r = r
        light.color.g = g
        light.color.b = b
```
