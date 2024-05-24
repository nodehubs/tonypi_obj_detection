# tonypi_obj_detection
# Function Introduction

This package identifies balls and pedestals using a deep learning method with the YOLOv5s model.

# Usage

## Preparations

1. Have a TonyPi robot, including a camera and RDK suite, and ensure it runs normally.
2. Prepare relevant props such as small balls.

## Install the Package

**1. Install the package**

After starting the robot, connect to the robot through terminal SSH or VNC, click the "One-click Deployment" button at the top right of this page, copy the following command to run on the RDK system to complete the installation of the relevant Node.

```bash
sudo apt update
sudo apt install -y tros-tonypi-obj-detection
```
**2. Run the Task Decomposition Function**

```shell
source /opt/tros/local_setup.bash

# Visualize the guide line midpoint on the web (after starting the function, open ip:8000 in the browser)
export WEB_SHOW=TRUE

ros2 launch tonypi_obj_detection target_detection.launch.py
```

# Principle Overview
The RDK X3 obtains environmental data in front of the robot through the camera. Image data is inferred using a trained YOLO model to get the image coordinates of objects and publishes them.

# Interface Description

## Topics

### Published Topics

|Name  | Type                                  |  Description           |
|------| --------------------------------------| --------------------------------|
|/robot_target_detection |ai_msgs::msg::PerceptionTargets | Publishes information about obstacles|

### Subscribed Topics

|Name  | Type                                  |  Description           |
|------| --------------------------------------| --------------------------------|
|/hb_image |hbm_img_msgs/msg/HbmMsg1080P| Image message published by the image correction node (640x480)|


## Parameters
| Parameter Name             | Type       | Description  |
| --------------------- | ----------- | ----------------------------------------------------- |
| sub_img_topic	|string	|The name of the subscribed image topic. Configure according to the actual received topic name. Default value is /hb_image |
| config_file	|string	|Path to the configuration file. Configure according to the recognition situation. Default value is config/TonyPi_yolov5sconfig.json |

# Note
This package provides a model for recognizing objects in specific real-world scenarios. If you collect your own dataset for training, please replace the model accordingly.