## NEARMISS

A near miss, "near hit", "close call", or "nearly a collision" is an unplanned event that has the potential to cause, but does not actually result in human injury, environmental or equipment damage, or an interruption to normal operation.

This solution can be used to reduce the Near Miss incidents happening on the roads or the areas where people need to be away from vehicles such as Petrol Stations while the vehicle is in area to fill the fuel.


![NEARMISS](resources/NearMiss.png)

## Citations

* https://github.com/aj-ames/Hermes-Deepstream
* https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_C_Sample_Apps.html

## Index

1. [Introduction](#Introduction)
2. [Deepstream Setup](#Deepstream-Setup)
    1. [Install System Dependencies](#Install-System-Dependencies)
    2. [Install Deepstream](#Install-Deepstream)
3. [Running the Application](#Running-the-Application)
    1. [Clone the repository](#Cloning-the-repository)
    2. [Run with different input sources](#Run-with-different-input-sources)

## Introduction

NEARMISS Application consists of an Intelligent Video Analytics Pipeline powered by Deepstream and NVIDIA Jetson Nano and on top of that we have applied some deep learning techniques for the object detection.
Whenever any vehicle or person is detected and found near to each other it will render the detections are red.

## Deepstream Setup

This post assumes you have a fully functional Jetson device. If not, you can refer the documentation [here](https://docs.nvidia.com/jetson/jetpack/install-jetpack/index.html).

### 1. Install System Dependencies

```sh
sudo apt install \
libssl1.0.0 \
libgstreamer1.0-0 \
gstreamer1.0-tools \
gstreamer1.0-plugins-good \
gstreamer1.0-plugins-bad \
gstreamer1.0-plugins-ugly \
gstreamer1.0-libav \
libgstrtspserver-1.0-0 \
libjansson4=2.11-1
```

### 2. Install Deepstream

Download the DeepStream 5.0.1 Jetson Debian package `deepstream-5.0_5.0.1-1_arm64.deb`, to the Jetson device from [here](https://developer.nvidia.com/assets/Deepstream/5.0/ga/secure/deepstream_sdk_5.0.1_amd64.deb). Then enter the command:

```sh
sudo apt-get install ./deepstream-5.0_5.0.1-1_arm64.deb
```

## Running the Application

### 1. Clone the repository

This is a straightforward step, however, if you are new to git or git-lfs, I recommend glancing threw the steps.

First, install git and git-lfs

```sh
sudo apt install git git-lfs
```

Next, clone the repository

```sh
# Using HTTPS
git clone https://github.com/poojabhasin/NearMiss.git
```

Finally, enable lfs and pull the model

```sh
git lfs install
git lfs pull
```

### 2. Run with different input sources

The computer vision part of the solution can be run on one or many input sources of multiple types, all powered using NVIDIA Deepstream.

First, build the application by running the following command:

```sh
make clean && make -j$(nproc)
```

This will generate the binary called `ds-nearmiss-app`. This is a one-time step and you need to do this only when you make source-code changes.

Next, create a file called `inputsources.txt` and paste the path of videos or rtsp url.

```sh
file:///home/pooja/DCMainGate_20201103_161120.mp4
rtsp://admin:admin@172.16.1.1:554/streaming/channels/101
```

Now, run the application by running the following command:

```sh
./ds-nearmiss-app
```

Finally, add the url in `inputsources.txt` and start `./ds-nearmiss-app`.
