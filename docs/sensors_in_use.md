---
title: Sensors & Data Flow
---

# Sensors & Real-Time Data Flow

This project relies on a variety of onboard sensors to perceive and interact with its environment. 
These sensors not only enable navigation and perception but also serve as core inputs to our real-time ROS2-based modular pipeline. 
Each sensor stream is visualized and processed in our GUI dashboard, allowing the system to respond interactively to the surroundings.

---

## Sensor Modalities & Data Interpretation 🔍 

### 1. Depth Camera (OAK-D Pro)
- Captures RGB and depth images.
- Used in conjunction with the YOLOv8 object detector node to identify objects.
- The depth stream is used to estimate proximity to detected objects.
- Raw image topic: `/oakd/rgb/preview/image_raw`
- Processed detections are visualized on the GUI and published to `/yolo_image_raw`.

### 2. LiDAR (RPLIDAR A1M8)
- Used for 360° spatial awareness and obstacle mapping.
- LaserScan data is subscribed via `/scan` topic.
- GUI radar plot visualizes real-time obstacles.
- Helps verify if the robot has a clear path before executing commands.

### 3. IMU
- Provides linear acceleration and angular velocity in 3D.
- Subscribed from `/rpi_13/imu` topic.
- Plotted as two separate graphs (Linear Acceleration and Angular Velocity) in GUI.
- Used for analyzing movement behavior, identifying drifts or unexpected turns.

### 4. Microphone (arecord)
- Records short audio bursts every 4 seconds.
- Whisper.cpp processes the waveform and outputs transcribed commands.
- Published to `/voice_text` and parsed by the `command_parser_node`.

---

## 📈 Real-Time Data Visualization Pipeline

Each of the sensors has a corresponding ROS2 subscriber and is rendered in the GUI dashboard as follows:

- Camera feed: live RGB image view.
- YOLOv8: overlaid bounding boxes and object labels.
- LiDAR: dynamic radar-style polar plot.
- IMU: scrollable X, Y, Z plots for both linear and angular data.
- Microphone: displays latest transcription + parsed command.

---

## Data Processing Pipeline

```mermaid
graph TD
  subgraph Perception
    CAM[OAK-D Camera RGB] --> DET[YOLOv8 Detection Node]
    DET -->|/yolo_image_raw| GUI1[GUI Display]
    MIC[Microphone Input] --> WHISPER[Whisper cpp Transcriber]
    WHISPER -->|/voice_text| CMD_PARSER[Voice Command Parser]
  end

  subgraph State Feedback
    IMU[IMU Data] -->|/rpi_13/imu| GUI2[IMU Plotting]
    LIDAR[RPLIDAR A1M8] -->|/scan| GUI3[Lidar Plot]
  end

  CMD_PARSER -->|/voice_command| ACTIONS[Action Trigger Node]
  DET -->|Detected Objects| GUI4[Object List Display]
```




### **TurtleBot 4 Sensor Table**  

### **TurtleBot 4 Sensor Table**

| **Sensor**               | **Implementation**                              | **Sensor Image**                                                                                                                                  | **Corresponding Plot** |
|--------------------------|--------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| **Depth Camera – OAK-D-Pro** | Object detection and distance estimation           | ![Depth Camera](https://github.com/user-attachments/assets/c8d24fc5-43ca-472e-8b87-457bf03e5386)                                             |![Picture1](https://github.com/user-attachments/assets/f6197cbe-517e-4a3b-9241-3d65ccb5c4ac)  |
| **LiDAR – RPLIDAR A1M8**     | Environment mapping, object distance & navigation | ![LiDAR](https://github.com/user-attachments/assets/61bd3394-74c4-4f4c-b989-9d63fbd989a9)                                                     | ![image](https://github.com/user-attachments/assets/493433f1-17ae-4e12-b67b-332163f545a4) |
| **IMU**                  | Motion state feedback and dynamic stabilization  | ![IMU](https://github.com/user-attachments/assets/3e5b5011-147c-44e6-b5ac-66b6b46a7fa6)                                                            | ![image](https://github.com/user-attachments/assets/a533e9a3-0bf9-40f5-8d52-ab0f54c05c23) |
| **Microphone**           | Capturing user speech for transcription          |  ![whispercpp](https://github.com/user-attachments/assets/7f51fb1c-d37c-4c93-96e5-7fd147a1d141)                                                    | ![image](https://github.com/user-attachments/assets/6daf667b-76c5-4b7f-abd9-2970b01dcfdc) |







