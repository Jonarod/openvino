Intel® OpenVINO™ in docker !

### Quick start

```
docker run --rm -it -v "$(pwd):/home" jonarod/openvino /bin/bash
```
(the image is 3GB in total so... grab a coffee...)

Then follow the docs to play around: [OpenVino Docs](https://docs.openvinotoolkit.org/latest/index.html)


### Run the the container with X enabled (Linux)

To run a sample application that displays an image, you need to share the host display to be accessed from guest Docker container.

The X server on the host should be enabled for remote connections:


```
xhost +
```


To run the sample-app image with the display enabled:

```
docker run --rm \
    --net=host \
    --env="DISPLAY" \
    --volume="$HOME/.Xauthority:/root/.Xauthority:rw" \
    -v "$(pwd):/home" \
    -it jonarod/openvino /bin/bash
```

Finally disable the remote connections to the X server

```
xhost -
```


### Build the image again

Download Intel® OpenVINO™ Toolkit: [https://software.intel.com/en-us/openvino-toolkit/choose-download/free-download-linux](https://software.intel.com/en-us/openvino-toolkit/choose-download/free-download-linux)

Then extract the zip (put the resulting folder next to the Dockerfile):

```
tar -xf l_openvino_toolkit*
```

Then build the image:

```
docker build -t <username>/openvino .
```

(Wait quite a bit... like 25mn in my i5 CPU)

