---
title: Voice Control
---

We implemented speech recognition on the TurtleBot4 system using Whisper.cpp – a lightweight, high-performance C++ implementation of OpenAI’s Whisper model. 
It enables voice-to-text transcription directly on-device, eliminating the need for cloud services and internet connectivity.

![Speech Recognition Whisper.cpp](https://github.com/user-attachments/assets/322549a8-430d-4813-ba16-4358e8d69257)

### How It Works 💬 

- The microphone on the host computer or external USB mic records a short audio clip (4 seconds).
- The audio is saved temporarily as a `.wav` file.
- Whisper.cpp processes this audio file using the `base.en` model to generate a transcription.
- The transcribed text is published to the ROS 2 topic `/voice_text`.

This node runs periodically and enables seamless integration of voice control into our ROS2 pipeline.

### 🛠️ Tradeoffs

- We initially tried online Whisper APIs, but due to computational load and latency, we switched to Whisper.cpp for real-time inference.
- Tiny model was fast but inaccurate for short commands. We upgraded to the base model for better transcription at the cost of minor latency.

### Live Demo 🧭

![image](https://github.com/user-attachments/assets/0352d36e-0342-45ec-ae20-7a3a02cd2128)




### ROS 2 Topics Used

- Subscribed: None
- Published: `/voice_text` (std_msgs/msg/String)

### ROS 2 Topic Flow 🧭 

```mermaid
graph TD
  mic_listener_node[mic_listener_node]
  voice_text[/voice_text/]
  command_parser_node[command_parser_node]
  voice_cmd[/voice_command/]
  movement_controller_node[movement_controller_node]

  mic_listener_node --> voice_text
  voice_text --> command_parser_node
  command_parser_node --> voice_cmd
  voice_cmd --> movement_controller_node
```
