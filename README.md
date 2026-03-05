# pid-bayesian-optimization

Bayesian Optimization framework for automatic tuning of PID controllers in a 6-axis robotic manipulator to improve reference trajectory tracking, while simultaneously estimating unknown link masses for accurate gravity compensation.

## Overview

This project explores the use of **Bayesian Optimization (BO)** to automatically tune **PID controllers** for a 6-axis robotic manipulator while simultaneously estimating unknown **link masses** used in the gravity compensation model.

The objective is to improve **trajectory tracking performance** when the dynamic parameters of the robot are not fully known. Instead of manually tuning the controller gains, Bayesian Optimization is used to systematically search for parameters that minimize the tracking error observed during trajectory execution.

The optimization procedure jointly estimates:

- PID gains for the joint controllers
- link masses used for gravity compensation

This allows the controller to achieve improved tracking performance while reconstructing part of the robot's dynamic model.

---

## Problem Description

The robotic system considered in this project is a **6-DoF manipulator** controlled in joint space using independent **PID controllers**.

Two main sources of uncertainty affect the system:

- PID gains were initially not tuned
- link masses required for gravity compensation were unknown

These factors result in degraded trajectory tracking and inaccurate compensation of gravitational effects.

The goal of the project is therefore to determine a set of parameters that minimizes the tracking error while ensuring stable and smooth robot motion.

---

## Methodology

### Control Architecture

Each joint is controlled using a standard **PID controller**

\[
\tau = K_p e + K_i \int e dt + K_d \frac{de}{dt}
\]

where

- \(e\) is the joint position error
- \(K_p, K_i, K_d\) are the PID gains
- \(\tau\) is the commanded torque

A gravity compensation term is included in the control loop using a simplified dynamic model. Since the **true link masses were not known**, they are treated as optimization variables.

---

### Optimization Variables

The Bayesian Optimization process searches for an optimal set of parameters including

- PID gains
- link masses used in the gravity model

These parameters are optimized simultaneously to minimize trajectory tracking error.

---

### Objective Function

The performance of each parameter set is evaluated using the **trajectory tracking error** during the execution of a reference motion.

A typical cost function used in the optimization is

\[
J = \frac{1}{T} \int_0^T \| q(t) - q_{ref}(t) \|^2 dt
\]

where

- \(q(t)\) is the measured joint position
- \(q_{ref}(t)\) is the reference trajectory
- \(T\) is the trajectory duration

---

## Results

The Bayesian Optimization procedure led to

- improved trajectory tracking accuracy
- automatic tuning of PID gains
- consistent estimation of link masses
- better gravity compensation performance

The optimization converged in a limited number of iterations thanks to the sample-efficient exploration strategy of Bayesian Optimization.

---

## Tools

The project was implemented and tested using

- **MATLAB**
- robotic simulation environment
- Bayesian Optimization tools

---

## Author

Matteo  
MSc Mechanical Engineering – Mechatronics and Robotics  
Politecnico di Milano
