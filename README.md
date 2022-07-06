# ROS package for YOLOv6

This repo contains a ROS noetic package for YOLOv6. It wraps the [official 
implementation](https://github.com/meituan/YOLOv6) into a ROS node (so most credit 
goes to the YOLOv6 creators).

![Example image from RVIZ](rviz_dogs.png)

## Requirements & Getting Started

Following ROS packages are required:
- [vision_msgs](http://wiki.ros.org/vision_msgs)
- [geometry_msgs](http://wiki.ros.org/geometry_msgs)

First, clone the repo into your catkin workspace and build the package:
```
git clone https://github.com/lukazso/yolov6-ros.git ~/catkin_ws/src/
cd ~/catkin_ws
catkin build yolov6-ros
```

The Python requirements are listed in the `requirements.txt`. You can simply 
install them as
```
pip install -r requirements.txt
```

Download the YOLOv6 weights from the [official repository](https://github.com/meituan/YOLOv6).

The package has been tested under Ubuntu 20.04 and Python 3.8.10.

## Usage
Before you launch the node, adjust the parameters in the 
[launch file](launch/yolov6.launch). For example, you need to set the path to your 
YOLOv6 weights and the image topic to which this node should listen to. The launch 
file also contains a description for each parameter.

```
roslaunch yolov6-ros yolov6.launch
```

Each time a new image is received it is then fed into YOLOv6.

### Notes
- The detections are published using the [vision_msgs/Detection2DArray](http://docs.ros.org/en/api/vision_msgs/html/msg/Detection2DArray.html) message type.
- The detections will be published under `/yolov6/out_topic`.
- If you set the `visualize` parameter to `true`, the detections will be drawn into 
  the image, which is then published under `/yolov6/out_topic/visualization`.

## Coming Soon
- Additional weights for automotive datasets
