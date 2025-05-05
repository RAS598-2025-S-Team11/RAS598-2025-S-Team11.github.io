---
title: Object Detection Page
---

## Object Detection with YOLOv8 🔎 

We implemented object detection using the YOLOv8 Nano model by Ultralytics, selected for its balance of speed and accuracy on resource-constrained hardware like the Raspberry Pi. This model performs real-time object detection from the Oak-D camera feed and publishes annotated frames along with recognized object labels.

![1_HctUSTC6_-OSWmCtTwmdeQ](https://github.com/user-attachments/assets/33f51c79-4182-433f-97ee-b8286003cb4a)


The detection results are displayed live on our custom GUI, and the recognized labels are also logged and published to a ROS 2 topic for downstream decision-making. This enables both GUI-based visualization and voice-interactive robot behavior based on perceived objects.

---

Some Object Dection Results:

![image](https://github.com/user-attachments/assets/a072299d-599e-44fd-83af-57bc3d5076bb)

![image](https://github.com/user-attachments/assets/4d4f89b8-6199-4877-95b8-57b85510e366)

