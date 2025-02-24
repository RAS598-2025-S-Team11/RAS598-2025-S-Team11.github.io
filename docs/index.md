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
- **Email:** anushka.satav@asu.edu

---
## Project Plan

> Research Question: 
> How can a mobile robot effectively combine vision, speech, and autonomous navigation to create a responsive and interactive system in real-world environments?

**Concept:** 

This project explores how TurtleBot4 can intelligently interact with its surroundings through vision-based object detection and speech-based communication. Using **TurtleBot 4 with Create 3 and Raspberry Pi**, our aim is to integrate:  

- **Real-time object detection** using **YOLOv8** for recognizing and categorizing objects in the environment.  
- **Voice command interaction** for user control, allowing spoken instructions to guide the robot's behavior.  
- **Autonomous navigation** with obstacle avoidance, ensuring safe and efficient movement in dynamic spaces.  
- **Dynamic responses** based on detected objects, enabling context-aware robotic actions.  
- **Fallback mechanisms** for handling hardware/software limitations and ensuring system robustness.  

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
| **Week 16** | **Apr 28, 2025**  | 🚀 **Final Demonstration & Project Submission** 🎯  | 🚀 Upcoming |

---
## Gantt Chart Representation 
```mermaid
gantt
    title Project Timeline (Weeks 7-16)
    dateFormat  YYYY-MM-DD
    section Planning
    Finalizing Scope :done, milestone1, 2025-02-24, 2d
    section Implementation
    ROS2 Setup :active, milestone2, 2025-03-03, 3d
    Object Detection :milestone3, 2025-03-10, 5d
    Speech Recognition :milestone4, 2025-03-17, 5d
    Navigation Testing :milestone5, 2025-03-24, 4d
    Integration & Debugging :milestone6, 2025-03-31, 7d
    section Testing & Deployment
    Real-World Testing :milestone7, 2025-04-07, 4d
    Final Prep :milestone8, 2025-04-14, 6d
    Documentation & Review :milestone9, 2025-04-21, 3d
    Final Demonstration :milestone10, 2025-04-28, 1d
```
