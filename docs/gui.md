---
title: GUI Updates
---

# GUI Modifications and Walkthrough

Over the course of the project, the PyQt5-based GUI evolved significantly as we integrated new sensors, added voice command capabilities, and refined real-time feedback. This table summarizes the development timeline and features added to each version.

---

## Evolution of the GUI

| **GUI Version**                        | **Screenshot**                                                                                                                                                      | **Description** |
|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| 🧪 Initial Mockup (Inkscape Plan)       | ![Mockup](https://github.com/user-attachments/assets/069d103c-103e-4c88-a693-fd7bdd21b459)                                                                           | A visual sketch designed using Inkscape to decide the layout and component flow of the final GUI. |
| 🎛️ First Working GUI Based on Mockup       | ![Proposed GUI](https://github.com/user-attachments/assets/fb130357-8975-4d73-b05b-b7d9f37f7a61)                                                                           | The first Interactive GUI for manual keyboard control and object detection  |
| 📉 GUI with IMU Plotting               | ![IMU GUI](https://github.com/user-attachments/assets/b1b43848-33e1-435c-b1bd-480aac67d069)                                                                           | Real-time IMU data plotting added using ROS2 `/rpi_13/imu`. Displays acceleration and angular velocity. |
| 🧭 GUI with LiDAR Integration          | ![LiDAR GUI](https://github.com/user-attachments/assets/cebbeee1-7b54-4118-8094-66bc6d0dcb0c)                                                                         | LiDAR scan data shown in a circular radar-style map. Helps visualize obstacle proximity around TurtleBot4. |
| 🧪 First Fully Integrated GUI          | ![MYU FINAL GUI](https://github.com/user-attachments/assets/8a287965-9850-4afe-82e7-7ecfd774a1b3)                                                                       | Combined real-time image feed, object detection, IMU, LiDAR, voice transcription, and parsed commands. |
| 🧠 Full System Integration GUI         | ![Final GUI](https://github.com/user-attachments/assets/3e7af140-66c6-4675-96dc-92d3f298474b)                                                                         | Combined real-time image feed, object detection, IMU, LiDAR, voice transcription, and parsed commands. |
| 🎛️ Basic GUI (Test 1)                  | ![Empty GUI](https://github.com/user-attachments/assets/0c15b374-2ac2-466d-816b-6da410848007)                                                                        | First working version with raw image display and placeholder for object detection overlay. No sensor plots or interactivity. |
| 🎯 Final Professional GUI              |  ![Data GUI](https://github.com/user-attachments/assets/4707b81f-a5d7-4002-89ff-bbb62c0ab408)                                                              | Fully optimized layout with color-coded feedback, buttons for voice fallback, dock/undock integration, and live object list. |

---

This version-controlled design process helped us meet technical requirements while making the GUI intuitive and powerful for both debugging and live demonstration use.

