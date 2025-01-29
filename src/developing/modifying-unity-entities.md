# Modifying Unity Entities  

Unity entities can be modified using the Unity Editor, which can be downloaded via the Unity Hub. These entities are defined in the [Duckiematrix](https://github.com/duckietown/duckiematrix) repository (currently private).  

```{note}
To ensure compatibility, install the same version of the Unity Editor as the branch you intend to edit. For example, if you are working on the `2022.3.20f1` branch, you should install Unity version `2022.3.20f1`.  
```

## Adding Sensors to an Entity  

This video demonstrates how to add a time-of-flight sensor to the DD24 entity. Since the C# class associated with the DD24 Unity entity inherits from `RobotAbs`, it already includes code to process data from a time-of-flight sensor.  

To add a sensor, define a unique name for it and specify its location and orientation within the entity.
```{todo}
Improve this
```

```{vimeo} 1051182529
```