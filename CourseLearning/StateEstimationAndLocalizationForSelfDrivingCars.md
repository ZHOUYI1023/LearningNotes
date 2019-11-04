## Least Squares
Assumption:
* linear measurement model
* measurements are eqaully weighted

Weighted Least Squares:
The higer the expected noise. the lower weight placed on the mwasurement

Recursive Least Squares:
online estimation
minimize tthe covariance of the parameters at the current time
form the update step for the linear Kalman Filter

## Maximum Likelihood
$\hat{x}_{MLE} = \argmax_x{p(y|x)} = \argmax_x{\log{p(y|x)}}$
since the logarithm is monotonically increasing
resulting in
$\log{y|x} = -\frac{1}{2R}((y_1-x)^2+...+(y_m-x)^2)+C = \argmin_x\frac{1}{2\sigma^2}((y_1-x)^2+...+(y_m-x)^2)$ 
Thus maximize the likelihood is equivalent to minimize the (weighted) least square error
if the noise is Gaussian white noise (Central Limit Theorem)
Least square estimates are significantly affected by outliers

## Kalman Filter
* Linear Kalman Filter
Prediction using motion model
Correction using measurement model

Bias in State Esitmation:
considering error dynamics, if the error expect is zero, than the prediction is unbiased

Consitent in State Estimation:
Estimated covariance is consistent with the empirical covariance
The filter is neither over-confident or under-confident

Linear Kalman Filter is BLUE: Best Linear Unbiased Estimator

## Extended Kalman Filter
 Linearizing a nonlinear system: choose an operating point and approximate the nonlinear function by a tangent line at that point (first order Taylor expansion)

 For EKF, we choose the operating point to be our most recent state esitmation, our known input and zero noise

 Jacobian Matrix
==vanilla EKF==

* The Error State Extended Kalman Filter (ES-EKF)
True State = Nominal State (Large) + Error State (Small)
$x = \hat{x} + \delta x$
Estimate the error state directly and use it as a correction to the nominal state
Reasons:
* the small error state is more amenable to linear filtering than the large nominal state, which can be integrated nolinearity
* easy to work with constrained quantities (e.g. rotation in 3D)

EKF is prone to linearization error when
1. the system dynamics are highly dynamics
2. the sensor sampling time is slow relative how fast the system is envolving

Linearization error can cause the estimator to be overconfident in a wrong answer
For highly nonlinear system, the EKF estimate can diverge and become unreilable
Computing Jacobian is error-prone

## Uncented Kalman Filter
The Uncented Transform: it is easier to approximate a probability distribution than it is to approximate an arbitary nonlinear function

Choosing Sigmapoints: for N-dimensional PDF, we need 2N+1 sigma points

Prediction Step:
1. Compute sigma points
2. Propagate sigma points
3. Compute predicted mean and covariance

Correction Step:
1. Predict measurements from propagated sigma points
2. Estimate mean and covariance of predicted measurements
3. Compute cross-covariance and Kalman gain
4. Compute corrected mean and covariance

## Reference Frame
* Rotation:
    * Rotation Matrix
    * Unit Quaternions
    * Euler Angles --- Singulatity
Localization Frame:
* ECIF Earth-Centered Inertial Frame
    * Earth rotates about the z-axis
* ECEF Earth-Centered Earth-Fixed Frame
    * Rotate with the Earth

Navigation Frame
* NED North East Down
    * x True North
    * y True East
    * z Down (along gravity)
* NEU Frame East North Up
    * x True East
    * y True North
    * z Up

Sensor Frame

## GNSS/INS Sensing for Pose Estimation
IMU
* gyroscopes
MEMS
measure orientation rate
* accelerometers

GNSS Global Navigation Satelite Systems


