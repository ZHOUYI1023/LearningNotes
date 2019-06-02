# INS-Camera Calibration without Ground Control Points
by TUM
##I. Introduction
GPS corrected INS: **cm for the position and hundredths of a defree for the  orientation per hour**
used for aerial systems(mobile platform)
without photogrammetric calibration site
calibration site with a hign number of ground control points (GCP)
graph optimization framework instead of using BA

##II. Related Work

**hand-eye calibration**

**single-step**

**two-step**

**photogrammtric calibration site**

##III. INS-Camera Calibration
East, North, Up (ENU) coordinate systems

camera: YXZ Euler angles(yaw, pitch, roll)

synchrnozed in time and rigidly mounted

jointly calibration of the intrinsic camera parameter in conjunction with the mounting offset out of synchronized data from measurement flights

###1. Initilization:
generate camera pose from measured IMU pose and offsets from construction drawings
###2. SFM
###3. Graph Optimization
through g2o

#Online Temporal Calibration for Monocular Visual-Inertial Systems
by Shen Shaojie
