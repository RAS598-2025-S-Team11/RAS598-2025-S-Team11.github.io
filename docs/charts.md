## Project Visual Overview

| Section              | Chart Title                                | Description                                                                 |
|----------------------|---------------------------------------------|-----------------------------------------------------------------------------|
| **Timeline**        | Gantt Chart                                 | Shows weekly project phases from planning to deployment.                    |
| **Workflow**        | Project Workflow Chart                      | Displays the full robot pipeline from sensor data to GUI feedback.          |
| **System Control**  | System Architecture + ROS2 Nodes & Topics  | Visualizes ROS2 nodes and topics, including collision avoidance logic.      |
| **Future Work**     | Cobot Arm Integration Flow                  | Outlines the proposed pick-and-place functionality using a mounted arm.     |


## Gantt Chart – Project Timeline Overview

```mermaid
%%{ init: {
  "theme": "default",
  "themeVariables": {
    "taskTextColor": "#ffffff",
    "taskBorderColor": "#666666",
    "taskFill": "#444444",
    "fontSize": "14px",
    "gridColor": "#999999"
  },
  "gantt": {
    "barHeight": 30,
    "barGap": 5
  }
} }%%
gantt
    title Project Timeline (Weeks 7–16)
    dateFormat  YYYY-MM-DD
    axisFormat  %b %d

    section Planning
    Finalize Scope            :milestone1, 2025-02-24, 7d

    section Implementation
    ROS2 Setup                :milestone2, 2025-03-03, 7d
    GUI Development           :milestone3, 2025-03-10, 7d
    YOLOv8 + Oak-D            :milestone4, 2025-03-17, 7d
    Voice Command             :milestone5, 2025-03-24, 7d
    ROS2 Integration          :milestone6, 2025-03-31, 10d

    section Testing & Deployment
    TurtleBot Testing         :milestone7, 2025-04-10, 7d
    Final Debug               :milestone8, 2025-04-17, 5d
    Docs & Video              :milestone9, 2025-04-22, 5d
    Final Demo                :milestone10, 2025-04-28, 6d

```

## Main Project Pipeline 

- The flowchart below represents the overall working of our Intelligent TurtleBot4 system. 
- It starts with sensor data collection from the Oak-D camera, IMU, LiDAR, and microphone. 
- The data is then preprocessed and sent to two parallel modules: YOLOv8 for object detection and voice recognition for interpreting commands.

- Outputs from both modules are fed into a decision-making node that determines the robot's next action. 
- The chosen action is executed via the ROS2 navigation stack and published as movement commands. 
- Simultaneously, the GUI updates with relevant feedback, allowing users to visualize object info and robot behavior in real time.


```mermaid
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

  A --> B --> C
  C --> D1 --> E
  C --> D2 --> F
  E --> G
  F --> G
  G --> H --> I --> K --> M
  G --> J --> L --> M
```
---

## System Control and Autonomy Flow

- The diagram below presents the complete decision and control loop of our TurtleBot4 system.
- From user voice inputs and real-time camera feeds, data is collected, processed, and passed through an autonomy layer to issue movement commands.
- Each subsystem (sensor, processing, autonomy) is driven by dedicated ROS2 nodes communicating through standard topics.

```mermaid
graph TD

  %% Top-Level Flow
  A[TurtleBot4 Booted]
  B[Sensor Data Collection]

  A --> B

  %% Sensor Layer
  subgraph Sensor_Layer [ROS2: Sensor Layer]
    N1[Node: oakd_camera_node] --> T1[/rpi_13/oakd/preview/image_raw/]
    N2[Node: voice_input_node] --> T2[/voice_input/]
  end

  %% Processing Layer
  subgraph Processing_Layer [ROS2: Perception & Command Parsing]
    N3[Node: yolov8_processor] --> T3[/yolov8_detections/]
    N4[Node: voice_command_parser] --> T4[/voice_cmd/]
  end

  %% Autonomy Layer
  subgraph Autonomy_Layer [ROS2: Autonomy & Control]
    N5[Node: decision_maker_node]
    N6[Node: collision_avoidance_node]
    N7[Node: navigation_controller]
    T5[/action_cmd/]
    T6[/cmd_vel/]
    N5 --> T5
    N5 --> N6 --> N7 --> T6
  end

  %% Flow between subgraphs
  B --> Sensor_Layer --> Processing_Layer --> Autonomy_Layer
  C[Turtlebot4 Output]
  Autonomy_Layer --> C

```
---
## Hybrid ROS2 System Architecture

- This diagram separates high-level autonomy (top row) from low-level motion control (bottom row), with clearly labeled ROS2 nodes and topic communication.
- It maintains modular blocks for perception, decision-making, and actuation while improving visual alignment and clarity.


```mermaid
graph TD

  %% Sensors
  subgraph SENSORS [Sensor Inputs]
    CAM[Oak-D Camera]
    MIC[Microphone]
    LIDAR[IR / LiDAR Sensors]
  end

  %% Perception Layer
  subgraph PERCEPTION [Perception Nodes]
    YOLO[Node: yolov8_processor]
    VOICE_RAW[Node: voice_input_node]
    YOLO_OUT[/yolov8_detections/]
    VOICE_IN[/voice_input/]
    CAM --> YOLO --> YOLO_OUT
    MIC --> VOICE_RAW --> VOICE_IN
  end

  %% High-Level Autonomy
  subgraph HIGH_AUTO [High-Level Autonomy]
    VOICE_PARSER[Node: voice_command_parser]
    VOICE_CMD[/voice_cmd/]
    DECIDE[Node: decision_maker_node]
    ACT_CMD[/action_cmd/]
    VOICE_IN --> VOICE_PARSER --> VOICE_CMD
    YOLO_OUT --> DECIDE
    VOICE_CMD --> DECIDE --> ACT_CMD
  end

  %% Low-Level Autonomy
  subgraph LOW_AUTO [Low-Level Control]
    COLL_AVOID[Node: collision_avoidance_node]
    NAV_CTRL[Node: navigation_controller]
    CMD_VEL[/cmd_vel/]
    LIDAR --> COLL_AVOID
    ACT_CMD --> COLL_AVOID --> NAV_CTRL --> CMD_VEL
  end

  %% Actuation
  CMD_VEL --> TBOT[TurtleBot Movement]

  %% Block-to-block flow
  SENSORS --> PERCEPTION --> HIGH_AUTO --> LOW_AUTO --> TBOT
```
---

## Future Work Concept: TurtleBot4 with Mounted Cobot Arm

This future work visual outlines the integration of a robotic arm on TurtleBot4. 
The system uses object detection and coordinates from the perception pipeline to compute inverse kinematics and execute pick-and-place actions via a dedicated ROS2 control node.

Goals to Capture Visually:
- Addition of a robotic arm mounted on TurtleBot4
- Use of ROS2 for communication with the arm
- Performing pick-and-place tasks
- Integration with existing perception (e.g., YOLOv8 object detection for picking targets)

```mermaid
graph TD

  %% Object Detection & Localization
  V1["Object Detection<br/>using YOLOv8"]
  V2["Target Object<br/>Coordinates"]

  %% Motion Planning
  M1["Inverse Kinematics<br/>& Arm Planning"]

  %% Platform Base
  P2["TurtleBot4 Base Platform"]
  P1["Mounted Cobot Arm<br/>on Platform"]

  %% ROS2 Control
  N1["ROS2 Arm<br/>Control Node"]

  %% Execution
  E1["Pick and Place<br/>Execution"]
  E2["Object<br/>Grasped and Placed"]

  %% Connections
  V1 --> V2 --> M1 --> N1
  P1 --> P2 --> N1
  N1 --> E1 --> E2
```


---


