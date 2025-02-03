(custom-map)=
# Custom Map

While the sandbox is nice and easy to use, it can get boring.
In this section, we will discuss how to run the Duckiematrix using a custom map.


(obtain-a-map)=
## Obtain a map

You can design your own map using the Duckietown Map Editor, which you can run with:

    dts map editor

```{todo}
link to the Map editor documentation
```

Alternatively, you can download a very simple map from [this link](https://duckietown-public-storage.s3.amazonaws.com/assets/duckiematrix/maps/loop.zip).
In this case, unzip the archive so that the file `main.yaml` is located at `~/loop/main.yaml`.


(use-custom-map)=
## Use a custom map

Assuming that you have your map ready to go at `~/loop`, remembering that a map is defined by a directory containing all the layers (YAML files) that form the map, you can launch an instance of the Duckiematrix using your map with:

    dts matrix run --standalone -m ~/loop

The command above will spin up an engine and renderer using your map.
Experiment with changing the map by, for example, rotating the tiles, by changing the `yaw` angle in the `frames.yaml` layer.
Note that, for any changes in the layers to appear in the renderer, the above command will need to be re-run.
