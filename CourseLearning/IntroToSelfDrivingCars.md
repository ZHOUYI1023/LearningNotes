## Taxonomy of Driving
* Level 1 - Driving  Assistant
Either longitudinal control or lateral control
examples: ACC, LKA
* Level 2 - Partial Driving Automation
Both longitudinal and lateral control
example: GM Super Cruise
* Level 3 - Conditional Driving Automation
included automated object and event detection and response (OEDR)
example: Audi A8
* Level 4 - High Driving Automation
Hnadles emergencies aytonomously, driver can entirely focus on other tasks
still limited ODD
example: Waymo
* Level 5 - Full Driving Automation
Unlimited ODD
## Perception
* identification
* understanding motion

* Static objects:
    * road and lane markings (on-road)
    * curbs (off-road)
    * traffic lights (off-road)
    * road signs (off-road)
    * construction signs, obstructions, and more (on-road)
* Dynamic objects:
    * vehicles
        * 4 wheelers (cars, trucks)
        * 2 wheelers (motorbikes, bicycles)
    *pedestrians
* Ego localization
    * position
    * velocity, accleration
    * orientation, angular motion

Challenges:
* robust detection and segmentaion
* sensor uncertainty
* occlusion, reflection
* illumination, lens flare
* weather, precipitation
## Planning
Making decisions:
* Long term
* Short term
* Immediate

Typs of plannning
* reactive rule based planning
* predictive planning
## Sensors
Types:
* exteroceptive
    * camera
    * radar
    * lidar
    * ultrasonic
* proprioceptive
    * GNSS/IMU
    * wheel odometry
## Sensor Configuration
aggresive deceleration: 5 $m/s^2$
comfortbale deceleration: 2 $m/s^2$
stopping distance: $d = \frac{v^2}{2a}$

Examples:
* Highway:
    * emergency stop
    * maintain speed
    * lane change
* Urban
    * emergency stop
    * maintain speed
    * lane change
    * overtaking
    * turning, crossing at intersections
    * Passing roudabouts
## Software Architecture
* Environment Perception
    * localization
    * dynamic object detection -> tracking -> motion prediction
    * static object detection
* Environment Maps
    * Occupancy Grid Map
    * Localization Map
    * Detailed Road Map
==Lyft article==
* Motion Planning
    * Mission Planner
    * Behaviour Planner
    * Local Planner
* Vehicle  Controller
    * Velocity Controller
    * Steering Controller
* System Supervisor
    * Software Supervisor
    * Hardware Supervisor
## Safety
Safe Process:
* Deductive Analysis: fault tree analysis
* Inductive Analysis: Design & Process FMEA
* Exploratory Analysis: HAZOP (Hazard & Operability Study)

Safety Thresholds
* Fail safe: redundant functionality
* ==SOTIF==: all critical functionalities are evaluated for unpredictable scenarios

Testing
* Performance testing
* Requirements validation
* Fault injection testing
* Intrusive testing such as electromagnetic inference
* Durability testing and simulation based testing

Method
* Analytical safety
* Data driven safety: Disengagement rate

## Safety Frameworks
* Fault Tree Analysis (FTA)
    * Top down deductive failure analysis
    * Assign probabilities to fault leaves
    * Use logic gates to construct failure tree
* Failure Mode and Effects Analysis (FMEA)
    * Bottome up process to identify all the effects of faults in a system
    * Failure Mode: modes or ways in which a component of the system may fail
    * Effect Analysis: analyzing effects of failure modes on the operation of  the system
    * Catogorize by failure modes by priority
        * Severity (S)
        * Occurrence (O)
        * Detection (D)
        * Risk Priority Number $RPN = S \cdotp O \cdotp D$
    * Eliminate or reduce failures, starting with top priority
* HAZOP - a variation on FMEA
    * brainstorming approach
* ISO 26262
    * safety due to absence of unreasonable risk
    * only concerned about malfunctioning system
    * V model
    * Hazard and Risk Assessment (HARA)
* ISO/PAR 21448.1 SOTIF
    * Failure due to performance limitations and misuse
        * Sensor limitations
        * Algorithm failures/ insufficiencies
        * User misuse - overload, confusion
    * Designed for L0-2, can be extended into above 3
    * Extension of FUSA
            * V model
            * HARA
## Kinematic Modelling in 2D
Coodinate Frams
* inerial frame: fixed
* body frame
* sensor frame

Nonholonomic constraint: velocity is always tangent to path
$\dot y\cos\theta - \dot x\sin\theta = 0 $

## The Kinematic Bicycle Model
* Front wheel steering
* Reference point
    * center of front axle
    * center of gravity
    * center of rear axle
* Rear wheel reference point
    * Instantaneous center of rotation (ICR)
    * $\dot\theta = \omega = \frac{v}{R} = \frac{v\tan{\delta}}{L}$
    * $\delta$ wheel angle
    * $\dot x_r = v \cos(\theta)\\
   \dot y_r = v \sin(\theta)\\
   \dot \theta = \frac{v\tan\delta}{L}$
* if desired point at the center of the front axle
    * $\dot x_f = v \cos(\theta+\delta)\\
   \dot y_f = v \sin(\theta+\delta)\\
   \dot \theta = \frac{v\sin\delta}{L}$
   * $\delta$ is the front wheel angle
* if desired point at the center of the gravity (cg)
    * slip angle $\beta$
* state: $[x, y, \theta, \delta]$
* input: $[v, \varphi]$
* $\dot x_c= v \cos(\theta+\beta)\\
   \dot y_c= v \sin(\theta+\beta)\\
   \dot \theta = \frac{v\cos\beta\tan\delta}{L}\\
   \dot\delta = \varphi$
## Dynamic Modelling in 2D
* Translational: Suspension
* Rotational: Tyre Model
* Full Vehicle Modelling
## Longitudinal Vehicle Modelling
* simplified model: $m\ddot x= F_x - F_{aero} -R_x -mg\alpha$
* $F_{aero} = \frac{1}{2}C_a\rho A\dot x^2 = c_a\dot x^2$
* rolling resistance: $ R_x = N(\hat c_{r,0}+\hat c_{r,1}|\dot x| + \hat c_{r,2}\dot x^2) \approx c_{r,1}|\dot x| $
* powertrain dynamics
    * wheel
    * transmission
    * torque converter
    * engine
    * $J_e\dot \omega_e = T_{engine} - (GR)(r_{eff}F_{load})$
## Lateral Dynamics of Bicycle Model
* suppose longitudinal velocity is constant
* tyre slip models
    * for small type slip angles, the lateral tyre forces are approximated as a linear function of tyre slip angle
* state vector $x_{lat} = [y, \beta, \psi, \dot \psi]$, i.e. lateral position, side slip angle, yaw angle, yaw rate
* $\delta$ is driver steering command
* $\dot X_{lat} = A_{lat}X_{lat} + B_{lat}\delta$
## Vehicle Actuation
* main control task: to keep the vehicle on the defined path at the desired velocity
* steering system
* powertrain system
    * throttling model
    * braking model
## Tyre Model
* tyre slip angle
* tyre logitudinal slip (slip ratio)
    * skidding
    * spinning
    * locked
* tyre modeling
    * analytical 
        * Brush, Fiala, Linear
        * low precision but simple
    * numerical
        * lookup table
        * difficult to use by model-based control
    * Parameterized
        * Linear, Pacejka, Dugoff
        * need experiments for each specific tyre
        * formed by fitting model with data
## Vechicle Longitudinal Control
* simple control algorithms
    * lead-lag controller
    * PID controller
* complex control algorithms
    * nonlinear methods: feedback linearization, backstepping, sliding mode
    * optimization methods: model predictive control
* PID controller
    * $u(t) = K_P e(t) + K_I\int_0^t e(t)dt + K_D \dot e(t)$
    * $U(s) = (K_P + \frac{K_I}{s} + K_D s) E(s)$
* Cruise Control
    * Speed is controlled by throttling and braking to be kept at the reference speed
* High level controller
    * $\ddot x_des = K_P(\dot x_{ref} - \dot x)+K_I\int_0^t(\dot x_{ref} - \dot x) +K_D\frac{d(\dot x_{ref} - \dot x)}{dt}$
* Low level controller
    * throttle and brake inputs are calculated to track the desired acceleration
    * desired acceleration --vehicle dynamics--> engine torque --engine maps--> throttle angle
* Feedforward speed control
    * provide predictive response, non-zero offset
    * referenced velocity -> engine angular speed -> engine torque -> throttle angle ->throttle angle
## Vehicle Lateral Control
* Reference Path
    * straight line segments
    * waypoints
    * parameterized curves
* Control Design
    * Geometric Controllers
        * pure pursuit(carrot following)
        * Stanley
    * Dynamic Controllers
        * MPC
        * Sliding Mode
        * Feedback Linearization
    * Error
        * heading error
        * crosstrack error: distance from center of front axle to the closest point on path (position error)
## Geometric Lateral Control
* works well for linear tyre region
* Pure pursuit controller
* Stanley controller

## Model Predictive Control
* Numerically solving an optimization problem at each time step
* Receding horizon approach
* Explicitly handles constraints
* Computationally expensive
* Linear MPC
    * unconstrained, finite horizon, discrete time
    * ==LQR provides a closed form solution==
* Nonlinear MPC
    * No closed form solution, must be solved numerically