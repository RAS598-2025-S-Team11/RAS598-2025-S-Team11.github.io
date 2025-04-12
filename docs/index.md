---
title: Project Intelligent TurtleBot4 
tags:
- Robotics
- AI
- Object Detection
- Speech Recognition
---

## Team Information

- **Project Name:** Intelligent TurtleBot: Deep Learning-Based Object Detection and Voice-Guided Navigation
- **Team Number:** 11
- **Team Members:** Anushka Gangadhar Satav, Adithya Konda, Sameerjeet Singh Chhabra
- **Semester:** Spring 2025
- **University:** Arizona State University
- **Class:** RAS 598 Experimentation and Deployment of Robots
- **Professor:** Dr. Dan Aukes
- **Email:** anushka.satav@asu.edu, akonda5@asu.edu, schhab18@asu.edu

---
## Project Plan

> Research Question: 
> How can a mobile robot effectively combine vision, speech, and autonomous navigation to create a responsive and interactive system in real-world environments?

**Concept:** 

This project explores how TurtleBot4 can intelligently interact with its surroundings through vision-based object detection and voice-guided navigation. Using TurtleBot 4 with Create 3 and Raspberry Pi, our aim is to integrate and demonstrate the following capabilities:

- Real-time object detection using YOLOv8, recognizing and categorizing environmental objects with live camera input.
- Voice command interaction, allowing users to issue spoken instructions that influence robot behavior through a natural interface.
- Autonomous navigation with obstacle avoidance using the ROS2 navigation stack, enabling safe and efficient mobility.
- Decision-making based on perception, where voice commands and visual detections combine to guide task execution.
- Fallback mechanisms to ensure robustness and handle unexpected failures in hardware or software modules.
---

This updated scope aligns directly with our project deliverables — voice-guided, vision-aware autonomous robot control — and leaves room for seamless extension into manipulation and complex task planning.

---
## Project Workflow

The system operates by capturing data from multiple sensors, interpreting user commands, and performing autonomous navigation and feedback. The diagram below outlines the overall data and control flow of the TurtleBot4 system.

```mermaid
%%{ init: {
  "theme": "default",
  "themeVariables": {
    "fontSize": "14px",
    "primaryColor": "#ffffff",
    "edgeLabelBackground": "#ffffff"
  }
}}%%
graph TD
  A["Start:<br/>TurtleBot4 Powered On"]
  B["Sensor Layer:<br/>Oak-D Camera, IMU, LiDAR, Mic"]
  C["Sensor Data<br/>Preprocessing"]
  D1["YOLOv8<br/>Object Detection"]
  D2["Voice Command<br/>Recognition"]
  E["Detected Object Info"]
  F["Intent or Goal Command"]
  G["Decision-Making Node"]
  H["ROS2 Navigation Stack"]
  I["Movement Commands<br/>via /cmd_vel"]
  J["GUI Update:<br/>Object and Nav Info"]
  K["Actuator Response:<br/>TurtleBot Moves"]
  L["User Feedback:<br/>GUI Visualization"]
  M["End"]

  %% Flow
  A --> B
  B --> C
  C --> D1
  C --> D2
  D1 --> E
  D2 --> F
  E --> G
  F --> G
  G --> H
  H --> I
  I --> K
  K --> M
  G --> J
  J --> L
  L --> M

  %% Styling groups
  classDef startend fill:#f6e3f3,stroke:#c27ba0,color:#000
  classDef sensing fill:#d0f0ef,stroke:#5bbdbb,color:#000
  classDef processing fill:#e8eaf6,stroke:#7986cb,color:#000
  classDef decision fill:#fce4ec,stroke:#ec407a,color:#000
  classDef navctrl fill:#e0f7fa,stroke:#00838f,color:#000
  classDef gui fill:#ede7f6,stroke:#7e57c2,color:#000

  %% Assign node classes
  class A,M startend
  class B sensing
  class C,D1,D2,E,F processing
  class G decision
  class H,I,K navctrl
  class J,L gui

```
---
## Project Discussions
### 1. Sensor Fusion and Autonomous Decision-Making

The TurtleBot4 system leverages multiple data sources — including vision, audio, and LiDAR — to perform real-time perception and intelligent control. 
These data streams are handled through modular ROS2 nodes that contribute to both high-level autonomy and low-level motion control.

### 2. Sensor Inputs

- **Oak-D Camera** provides real-time RGB images for visual perception.
- **Microphone** captures user voice commands as audio input.
- **LiDAR and IR sensors** are used for obstacle detection and collision avoidance.

These sensors operate concurrently and feed their outputs into dedicated ROS2 nodes.

### 3. Perception and Processing Nodes

- `yolov8_processor`: Subscribes to image streams (`/rpi_13/oakd/preview/image_raw`) and outputs detected object data to `/yolov8_detections`.
- `voice_input_node`: Processes raw audio and converts it into structured voice data (`/voice_input`).
- `voice_command_parser`: Transforms audio into semantic commands (e.g., "move forward") and publishes them to `/voice_cmd`.

This layered perception setup allows the robot to understand both its **physical environment** and **human intent** simultaneously.

### 3.1 High-Level Autonomy

The core decision-making logic resides in the `decision_maker_node`, which:

- Consumes outputs from both `/yolov8_detections` and `/voice_cmd`
- Prioritizes user commands or detected objects to determine the appropriate action
- Publishes resulting commands to `/action_cmd`

### 3.2 Low-Level Motion Control

Low-level execution is handled by the following:

- `collision_avoidance_node`: Merges `/action_cmd` with real-time sensor data (e.g., LiDAR) to determine safe trajectories
- `navigation_controller`: Translates the motion plan into velocity commands published to `/cmd_vel`

These nodes form a closed-loop controller that ensures both **goal-directed behavior** and **safety**.

---
## 3.3 Control Architecture in ROS2

The following flowchart summarizes the control pipeline, organized by data type and decision layer:

```mermaid
graph TD

  subgraph "Sensor Inputs"
    CAM[Oak-D Camera]
    MIC[Microphone]
    LIDAR[IR / LiDAR Sensors]
  end

  subgraph "Perception Nodes"
    YOLO_NODE[Node: yolov8_processor]
    VOICE_NODE[Node: voice_input_node]
    DETECTIONS[/yolov8_detections/]
    VOICE_RAW[/voice_input/]
    CAM --> YOLO_NODE --> DETECTIONS
    MIC --> VOICE_NODE --> VOICE_RAW
  end

  subgraph "High-Level Autonomy"
    VOICE_PARSER[Node: voice_command_parser]
    VOICE_CMD[/voice_cmd/]
    DECISION[Node: decision_maker_node]
    ACT_CMD[/action_cmd/]
    VOICE_RAW --> VOICE_PARSER --> VOICE_CMD
    DETECTIONS --> DECISION
    VOICE_CMD --> DECISION --> ACT_CMD
  end

  subgraph "Low-Level Control"
    COLLISION[Node: collision_avoidance_node]
    NAV[Node: navigation_controller]
    CMD[/cmd_vel/]
    LIDAR --> COLLISION
    ACT_CMD --> COLLISION --> NAV --> CMD
  end

  CMD --> MOVE[TurtleBot Movement]
```
### 4. ROS2 and GUI

#### GUI Integration

The graphical user interface (GUI) plays a key role in closing the feedback loop between perception, autonomy, and user interaction. It provides real-time insights into the robot's internal state and sensory understanding.

The GUI displays:

- Real-time video feed with overlaid object detections from the onboard Oak-D camera
- Voice command recognition status and interpreted instructions
- Navigation and movement feedback, including direction, velocity, and planned path
- Sensor data such as LiDAR scans, IMU readings, and obstacle detections

The GUI is integrated with ROS2 and subscribes to the following key topics:

- `/yolov8_detections` – Visual object detection results
- `/voice_cmd` – Parsed user voice commands
- `/cmd_vel` – Velocity commands issued to the robot
- `/rpi_13/hazard_detection` – Safety and obstacle data
- `/rpi_13/imu` – Orientation and motion readings

This interface allows users to monitor system behavior in real-time, verify decision-making logic, and better understand the robot's perception and action in dynamic environments.

**1. Using Inkscape**

![image](https://github.com/user-attachments/assets/069d103c-103e-4c88-a693-fd7bdd21b459)

**2. Proposed GUI For Control**

![team-assignment-03-gui](https://github.com/user-attachments/assets/641e4521-9a4e-4248-9bda-127ad392c9cd)

**3. Proposed GUI For Navigation**
![task-2](https://github.com/user-attachments/assets/0ae545f4-2bab-45d4-878f-b5a7143b01e1)

---
## Demonstration Videos

### Test 01: Object Detection + GUI Overlay

[![Watch on YouTube](https://img.youtube.com/vi/hz7PwtZZgPg/0.jpg)](https://youtube.com/shorts/hz7PwtZZgPg?si=9SIvASX0w476p8vp)

*Real-time object detection using YOLOv8 with GUI overlay showing detected objects and confidence scores.*

---

### Test 02: Voice Command Navigation *(Coming Soon)*

_A short demo showcasing voice-command-based control of TurtleBot4 in a dynamic environment._

---

### Test 03: Full Autonomy Simulation *(Planned)*

_A future test combining voice input, object detection, and autonomous navigation on real hardware._

---
## Sensor Integration

**Utilization of Sensor Data**

![TurtleBotsFacing](https://github.com/user-attachments/assets/dfe928cf-b7cf-4cf4-82e4-b80c5853edfc)

> Check *Sensors Table* for more Information

- **Depth Camera (OAK-D/RealSense)**: Object detection and distance estimation.
- **LiDAR**: SLAM-based navigation and obstacle detection.
- **IMU**: Enhancing motion stability and drift correction.
- **Microphone**: Capturing voice commands.
- **Speaker**: Responding with audio feedback.

**Testing and Demonstration**

- **Unit Testing**: Each sensor tested in isolation.
- **Integration Testing**: Validating sensor fusion for decision-making.
- **Final Demonstration**: Robot detects objects, responds to queries, follows voice commands, and navigates autonomously.

---
## Interaction Mechanism

**Behavioral Influence & Interfaces**

- **Voice Command API**: Users instruct the robot using predefined phrases.
- **ROS2 RQT GUI/Web Dashboard**: For remote monitoring.

*(Include a professional-looking UI sketch showing how users will interact with the system.)*

## Control & Autonomy

- **Sensor-Driven Control Loop**: Robot makes decisions based on camera, LiDAR, and IMU inputs.
- **ROS2 Navigation Stack**: Used for path planning and movement.
- **Hierarchical Decision Model**: Combining high-level commands with low-level execution.



---
## Preparation Needs

### Required Knowledge & Topics for Success

- **Deep Learning for Object Detection** (YOLOv8, OpenCV)
  
  ![1_HctUSTC6_-OSWmCtTwmdeQ](https://github.com/user-attachments/assets/b6a43a67-39f3-478a-89bd-19b4d52bfc7f)

- **ROS2 Navigation & Collision Avoidance**
  
  ![turtlebot4](https://github.com/user-attachments/assets/688f6b41-9997-4dbe-bbdc-381155b9fe72)

- **Speech Recognition**
  
  ![download](https://github.com/user-attachments/assets/2f24f9f2-9335-4004-8189-de530818126a)

- **Hardware-Level Control for TurtleBot 4**
  
  Using communication between Host PC and TurtleBot4 to take Voice Commands as inputs and perform Pre-defined Actions

  ![images](https://github.com/user-attachments/assets/6b89eaaf-8b66-48bb-af69-54fefb0fac88)


---
## Final Demonstration Plan

### Setup & Execution

- **Classroom Resources**: Open space for navigation demo.
- **Demonstration Steps**: The robot will identify objects, respond to user queries, navigate obstacles, and execute spoken commands.

### Handling Environmental Variability (future scope)

- **Adaptive Algorithms**: Adjust object detection thresholds dynamically.
- **Fallback Modes**: If detection fails, switch to manual control or alternative recognition models.

### Testing & Evaluation Plan

- **Simulated Testing in Gazebo** before real-world deployment.
- **Comparison Metrics**:
  - Object recognition accuracy.
  - Speech command response time.
  - Navigation success rate.

---
## Impact

This project will:

- Advance AI-driven robotics interactions for smart environments.
- Develop speech-integrated autonomous systems.
- Provide students hands-on experience with ROS2, AI, and embedded systems.
- Potentially contribute to assistive robotics research.
---

---

### Future Scope:

In future iterations, the system can be extended with:

- Robotic arm integration mounted on TurtleBot4 for executing pick-and-place actions based on detected objects.
- Task-oriented planning using semantic understanding of scenes (e.g., pick red object and place it near the wall).

![image](https://github.com/user-attachments/assets/320d1ff7-a982-4fe4-ac4c-eabfbe49d17d)

![image](https://github.com/user-attachments/assets/d01f286a-b695-4d40-ac33-74acaa0e303e)


Here is the generated image of a cobot mounted on a TurtleBot4 using CHATGPT 4o




## References *(Subject to change)*:

1. Deep Learning model options: https://yolov8.com/
2. YOLOv8 example: https://rs-punia.medium.com/building-a-real-time-object-detection-and-tracking-app-with-yolov8-and-streamlit-part-1-30c56f5eb956
3. Speech Recognition Libraries: https://pypi.org/project/SpeechRecognition/
4. Turtlebot4 Mapping Resource: https://turtlebot.github.io/turtlebot4-user-manual/tutorials/generate_map.html
5. Mapping, Localizing, Path planning packages for Turtlebot4: https://turtlebot.github.io/turtlebot4-user-manual/tutorials/turtlebot4_navigator.html

---
## Advising & Resources

### Project Advisor

- **Dr. Daniel Aukes** 
- **Resource Needs**: Hardware support, mentorship on TurtleBot4 Hardware integration with ROS2.

---
# Weekly Milestones (Weeks 7-16)

| **Week**  | **Date**        | **Milestone**                                              | **Status**   |
|-----------|----------------|------------------------------------------------------------|--------------|
| **Week 7**  | **Feb 24, 2025**  | Finalizing project scope, confirming sensor availability.  | 🔄 In Progress |
| **Week 8**  | **Mar 3, 2025**   | Setting up ROS2 communication between Raspberry Pi and host machine.  | ⏳ Pending |
| **Week 9**  | **Mar 10, 2025**  | Implementing object detection pipeline.  | ⏳ Pending |
| **Week 10** | **Mar 17, 2025**  | Developing speech recognition module.  | ⏳ Pending |
| **Week 11** | **Mar 24, 2025**  | Testing navigation with LiDAR and obstacle avoidance.  | ⏳ Pending |
| **Week 12** | **Mar 31, 2025**  | Integrating all modules for unified control.  | ⏳ Pending |
| **Week 13** | **Apr 7, 2025**   | Conducting real-world tests and debugging issues.  | ⏳ Pending |
| **Week 14** | **Apr 14, 2025**  | Preparing final demonstration setup.  | ⏳ Pending |
| **Week 15** | **Apr 21, 2025**  | Final testing, documentation, and advisor review.  | ⏳ Pending |
| **Week 16** | **Apr 28, 2025**  | 🚀 **Final Demonstration & Project Submission** 🎯  | 🚀 Upcoming  |

---
## Gantt Chart Representation 
```mermaid
gantt
    title Project Timeline (Weeks 7-16)
    dateFormat  YYYY-MM-DD
    section Planning
    Finalizing Scope :active, milestone1, 2025-02-24, 7d
    section Implementation
    ROS2 Setup :active, milestone2, 2025-03-03, 7d
    Object Detection :milestone3, 2025-03-10, 7d
    Speech Recognition :milestone4, 2025-03-17, 7d
    Navigation Testing :milestone5, 2025-03-24, 7d
    Integrate & Debug :milestone6, 2025-03-31, 7d
    section Testing & Deployment
    Real-World Testing :milestone7, 2025-04-07, 7d
    Final Prep :milestone8, 2025-04-14, 7d
    Document & Review :milestone9, 2025-04-21, 7d
    Final Demonstration :milestone10, 2025-04-28, 6d
```
