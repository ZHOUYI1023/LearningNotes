# Computer Vision for Autonomous Vehicles: Problems, Datasets and State-of-the-Art

**Critical unsloved problems for autonomous vehicles:**
* operate in complex environment: need generalize to unpredictable situations
* accurate perception: 100% recall

**Bottlenecks:**
* Computing Power? Already sufficient
* Algorithm: need to reach human level reliability and react safely even in complex innercity situations
* Sensor Capbility: need to handle reflections, wet road, direct sunshine, tunnels and shadows
* Legal Issue: Responsibility 

## Datasets
* KITTI
* Cityscapes
### Real-World Datasets
* Stereo and 3D Reconstruction
    * Middelbury stereo benchmark
    * Middlebury multi-view stereo (MVS)
    * TUD MVS
* Optical Flow
    * Middlebury flow benchmark
* Object Recognition and Segmentation
    * 
* FLIR Thermal Dataset
## Cameras Models & Calibration
### Calibration
* Automatic calibration of range and camera sensors using a single shot
* Camodocal: Automatic intrinsic and extrinsic calibration of a rig with multiple generic cameras and odometry
* Leveraging image-based localization for infrastructure-based calibration of a multi-camera rig
### Omnidirectional Cameras
### Event Cameras
produce a stream of asynchronous events at microsecond resolution
low latency and low bandwidth requirement
* event to frame conversion
    * generate intensity images by accumulating events over a fixed time interval
    * introduces some latency
* exploit the high temporal resolution and the asynchronous nature
## Representations

### Superpixels

### Stixels

## Object Dectection

### Sensors
* Visible Spectrum (VS) Cameras & Laser Scanner
    * affected by reflective or transparent surfaces
* Thermal infrared (TIR) cameras
    * affected by hot objects like engines or warm temperature
