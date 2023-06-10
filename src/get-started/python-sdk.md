(python-sdk)=
# Python SDK

The Duckiematrix comes with a Python SDK that allows us to develop both environment and agent
behaviors.

```{todo}
Explain the SDK here
```
# Entities I/O
## Sensors

Sensors have a common API that comprises several methods we can call.

- To start the connection to a sensor that exists on the entity we want to connect to we use the method `.start()`

- To open the connection to a sensor that has been started we use the method `.attach()`. This method has a parameter `callback` that can be a `Callable` that processes the messages. We can add several callbacks using this method.

- To remove a callback from a sensor stream we can use the method `.detach()`, again providing it with the parameter `callback`.

- To close the connection to a sensor we have started, use the `.release()` method.

- Obtaining a message from a sensor can be done by using the `.capture()` method.

    This method accepts two parameters:

    - `block : bool = False` to make the driver wait (up to a timeout) to receive the frame before moving on.
    - `timeout: float = None` to specify the timeout for the `block` parameter.


### Camera
The camera API allows us to obtain images from the Duckiematrix.
The obtained images by default are JPEG-encoded. The API is available to any entity of type `CameraEnabledRobot`.

To obtain a frame from the camera we can use the method `.capture()`:

```python
msg : CameraFrame = CameraEnabledRobot.capture(block=True, timeout=1)
```

The obtained message is of type `CameraFrame` and has the following fields:

```python
CameraFrame

format: str  # Image format
width: int   # Width of the image in pixels
height: int  # Height of the image in pixels
frame: bytes # raw content of the image
```



### Time of Flight 
The Time of Flight sensors provide the range measured by the virtual entity.
In this case we can again use the `.capture()` method to obtain them and the message obtained will be of type `TimeOfFlightRange`:

```python
TimeOfFlightRange

range: float  # Time of flight range
```

#### Encoders
The encoders provide the ticks measured by the virtual entity.
In this case we can again use the `.capture()` method to obtain them and the message obtained will be of type `WheelEncoderTicks`:

```python
WheelEncoderTicks

ticks: int  # Encoder ticks
```

## Actuators

Actuators allow us to interact with the Duckiematrix environment. The Duckiebots have wheel motors to control the two wheels and LEDs to visually communicate with humans and other Duckiebots.

### Wheels driver

```{todo}
To update once the wheels communication protocol has been defined.
```

### LEDs
The LEDs configuration reflects the one of the Duckiebots, allowing to control 5 LEDs indexed from `0` to `4`.
In this case the object that allows us to manipulate all the different LEDs is of type `Lights`. This object contains each LED as a `LED` object; we can retrieve each LED object `i` by calling `<Lights>.light<i>`. 

Each LED object has a `color` property with 3 color channels (red `r`, green `g` and blue `b`) that can be set to a different value in the range `[0-255]`.
To do so we can use the `.atomic()` context, that automatically commits the changes to the engine to be displayed. An example is as following:

```python
with self.robot.lights.atomic():
    for light in self.robot.lights:
        light.color.r = r
        light.color.g = g
        light.color.b = b
```
