---
title: Project Workflow Chart
---

## Overview of Workflow 

```mermaid
graph TD
  A[Start] --> B[Sensor Data Acquisition]
  B --> C[Process Data]
  C --> D{Decision-Making}
  D -->|Object Detected| E[Trigger Response]
  D -->|No Object| F[Continue Scanning]
  E --> G[Voice Feedback]
  E --> H[Navigation Adjustment]
  H --> I[Obstacle Avoidance]
  I --> D
  G --> J[End]
  F --> B
```

## System Interaction Flow

```mermaid
sequenceDiagram
  autonumber
  User->>Robot: Provide Voice Command
  Robot->>Sensor Module: Capture Audio
  Sensor Module->>Processor: Process Speech
  Processor->>Decision Engine: Identify Intent
  Decision Engine-->>Robot: Execute Action
  alt Object Detected
      Robot->>User: Provides Object Information
  else No Object Found
      Robot->>User: Requests Clarification
  end
  Robot-->>Navigation Module: Adjust Path
  Navigation Module->>Robot: Confirm Path Update
  Robot->>User: Acknowledges Completion
```

## State Transitions in Navigation

```mermaid
stateDiagram-v2
  state scan_state <<fork>>
    [*] --> scan_state
    scan_state --> Object_Detected
    scan_state --> No_Object

    state decision_state <<join>>
    Object_Detected --> decision_state
    No_Object --> decision_state
    decision_state --> Navigate
    Navigate --> [*]
