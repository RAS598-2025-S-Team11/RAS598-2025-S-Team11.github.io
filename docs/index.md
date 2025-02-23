---
title: Intelligent TurtleBot for Real-Time Object Recognition, Voice Interaction and Safe Navigation
tags:
- Robotics
- AI
---

## Team Information

- Project Name: Intelligent TurtleBot: Deep Learning-Based Object Detection and Voice-Guided Navigation
- Team Number: 11
- Team Members: Anushka Gangadhar Satav, Samarjeet, Adithya Konda, Sameerjeet Singh Chhabra
- Semester: Spring 2025
- University: Arizona State University
- Class: RAS 598 Experimentation and Deployment of Robots
- Professor: Dr. Dan Aukes
- Email- anushka.satav@asu.edu

---
## Project Plan

### Concept: 
This project explores how a mobile robot can intelligently interact with its surroundings through vision-based object detection and speech-based communication. Using **TurtleBot 4 with Create 3 and Raspberry Pi**, our aim is to integrate:  

- **Real-time object detection** using **YOLOv8** for recognizing and categorizing objects in the environment.  
- **Voice command interaction** for user control, allowing spoken instructions to guide the robot's behavior.  
- **Autonomous navigation** with obstacle avoidance, ensuring safe and efficient movement in dynamic spaces.  
- **Dynamic responses** based on detected objects, enabling context-aware robotic actions.  
- **Fallback mechanisms** for handling hardware/software limitations and ensuring system robustness.  


### Research Question: 
How can a mobile robot effectively combine vision, speech, and autonomous navigation to create a responsive and interactive system in real-world environments?

---
## Sensor Integration

### Utilization of Sensor Data

- **Depth Camera (OAK-D/RealSense)**: Object detection and distance estimation.
- **LiDAR**: SLAM-based navigation and obstacle detection.
- **IMU**: Enhancing motion stability and drift correction.
- **Microphone**: Capturing voice commands.
- **Speaker**: Responding with audio feedback.

### Testing and Demonstration

- **Unit Testing**: Each sensor tested in isolation.
- **Integration Testing**: Validating sensor fusion for decision-making.
- **Final Demonstration**: Robot detects objects, responds to queries, follows voice commands, and navigates autonomously.

---
## Interaction Mechanism

### Behavioral Influence & Interfaces

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
- **ROS2 Navigation & Collision Avoidancve**
- **Speech Recognition**
- **Hardware-Level Control for TurtleBot 4**

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
## Advising & Resources

### Project Advisor

- **Dr. Aukes** 
- **Resource Needs**: Hardware support, mentorship on TurtleBot4 Hardware integration with ROS2.

---
## Weekly Milestones & Gantt Chart (Weeks 7-16)

| **Week** | **Milestone** |
|----------|--------------|
| **24-02-25**  | Finalizing project scope, confirming sensor availability. |
| **27-02-25**  | Setting up ROS2 communication between Raspberry Pi and host machine. |
| **03-03-25**  | Implementing object detection pipeline. |
| **03-03-25** | Developing speech recognition module. |
| **11-03-25** | Testing navigation with LiDAR and obstacle avoidance. |
| **15-03-25** | Integrating all modules for unified control. |
| **18-03-25** | Conducting real-world tests and debugging issues. |
| **21-03-25** | Preparing final demonstration setup. |
| **27-03-25** | Final testing, documentation, and advisor review. |
| **28-03-25** | Demonstration and final project submission. |
