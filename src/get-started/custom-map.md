(custom-map)=
# Custom Map

While the sandbox is nice and easy to use, it can get boring.
In this section, we will see how we can run the Duckiematrix on a custom map.


(obtain-a-map)=
## Obtain a Map

You can design your own map using the Duckietown Map Editor that you can run with the
command,

```{todo}
link to the Map editor documentation
```

```shell
dts map editor
```


Alternatively, you can download a very simple map from
[this link](https://duckietown-public-storage.s3.amazonaws.com/assets/duckiematrix/maps/loop.zip).
In this case, unzip the archive so that the file `main.yaml` is located at `~/loop/main.yaml`.



(use-custom-map)=
## Use a custom map

Let us assume that you have your map ready to go at the path `~/loop/`.
Remember, a map is defined by a directory containing all the layers (YAML files)
that form the map.

We can launch a Duckiematrix on our custom map using the command,

```shell
dts matrix run --standalone -m ~/loop/
```


The command above will spin up an engine and a renderer on your map.
Experiment with changing the map, for example by rotating the tiles by changing the `yaw`
angle in the `frames.yaml` layer.
Remember, you have to stop and re-run the command above for any changes in the layers to
appear in the renderer.
