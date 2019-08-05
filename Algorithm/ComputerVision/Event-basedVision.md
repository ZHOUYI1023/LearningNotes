# Event-based Vision: A Survey
## 1. Introduction and Applications
Event camera are asychronous sensors

Advantages:
- high temporal resolution (in microseconds)
- low latency (in microseconds)
- high dynamic range (over 140db)
- low power consumption

Scenarios:
- uncontrolled lighting conditions
- latency
- power limited

Applications:
- detection and tracking
    - object tracking
    - surveillance and monitoring
    - object recognition
    - gesture control
- ego-motion estimation
    - pose tracking
    - SLAM
- other cv tasks
    - depth estimation
    - 3D panoramic imaging
    - structured light 3D scanning
    - optical flow estimation
    - HDR image reconstruction
    - mosaicing
    - video compression
    - image debluring
    - star tracking

commercial production by **Samsung** and **Prophesee**

## 2. Principle of Operation of Event Cameras
Dynamics Vision Sensors(DVS)
data-driven sensors
output a variable data-rate sequence of digital events or spikes, with each event representing a change of brightness(log intensity) of predefined magnitude at a pixel at a particular time, inspired by the spiking nature of biological visual pathways

### 2.1 Event Camera Types