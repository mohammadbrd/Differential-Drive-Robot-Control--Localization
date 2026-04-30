<div align="center">

# 🤖 Differential Drive Robot Control & Localization

### MATLAB/Simulink project for trajectory tracking, feedback control, and observer-based localization of a differential-drive mobile robot

![MATLAB](https://img.shields.io/badge/MATLAB-Simulation-orange?style=for-the-badge&logo=mathworks)
![Simulink](https://img.shields.io/badge/Simulink-Control%20System-blue?style=for-the-badge)
![Robotics](https://img.shields.io/badge/Robotics-Mobile%20Robot-brightgreen?style=for-the-badge)
![Control](https://img.shields.io/badge/Control-State%20Feedback-purple?style=for-the-badge)

</div>

---

## 📌 Overview

This project focuses on the **control and localization of a differential-drive mobile robot** using MATLAB and Simulink. The robot is modeled as a nonlinear mobile platform with two independently driven wheels, and the project develops multiple controller and observer structures to improve trajectory tracking and state estimation.

The main goal is to move the robot along a desired reference path while maintaining stable behavior through modern control techniques such as **state feedback**, **pole placement**, **integral control**, and **observer-based estimation**.

---

## 🎯 Project Objectives

- Model the kinematics of a differential-drive mobile robot.
- Design feedback controllers for robot motion control.
- Track a predefined reference trajectory.
- Improve tracking performance using integral action.
- Estimate robot states using full-order and reduced-order observers.
- Test controller behavior under system variations and upgraded models.
- Validate the design using MATLAB/Simulink simulations.

---

## 🧠 Key Concepts

This repository combines several important concepts from robotics and control engineering:

| Area | Description |
|---|---|
| Differential-drive robotics | Motion of a two-wheel mobile robot with independent wheel velocities |
| State-space control | Modeling and control using matrices `A`, `B`, `C`, and `D` |
| Pole placement | Designing controller gains by assigning desired closed-loop poles |
| Integral control | Reducing steady-state tracking error by adding integral states |
| Observer design | Estimating unavailable states from measured outputs |
| MATLAB/Simulink simulation | Testing controllers and robot behavior in a simulation environment |

---

## 🛠️ Technologies Used

- **MATLAB**
- **Simulink**
- **Control System Toolbox**
- **State-space modeling**
- **Lyapunov equation methods**
- **Observer-based control**

---

## ⚙️ Control Design

The project uses a state-space model of the robot and applies feedback control to stabilize the system and follow a desired path.

The main MATLAB script defines the system matrices:

```matlab
A = [0 -pi/16 0;
     pi/16 0 3*pi/16;
     0 0 0];

B = [1/2 1/2;
     0 0;
     1/0.15 -1/0.15];

C = [1 0 0;
     0 1 0];

D = [0 0;
     0 0];
```

### State Feedback Controller

A pole-placement controller is designed using MATLAB's `place()` function:

```matlab
K1 = place(A, B, [-30 -1+4.899i -1-4.899i]);
```

This assigns the closed-loop poles to desired locations, improving the dynamic response of the robot.

### Integral Controller

To improve reference tracking and reduce steady-state error, the system is extended with integral states:

```matlab
A_bar = [0 -pi/16 0 0 0;
         pi/16 0 3*pi/16 0 0;
         0 0 0 0 0;
         1 0 0 0 0;
         0 1 0 0 0];

B_bar = [1/2 1/2;
         0 0;
         1/0.15 -1/0.15;
         0 0;
         0 0];

K_bar = place(A_bar, B_bar, [-60 -55 -70 -1+4.899i -1-4.899i]);
```

The resulting gain matrix is separated into:

```matlab
Ka  = K_bar(:,4:5);   % Integral gains
K_f = K_bar(:,1:3);   % State feedback gains
```

---

## 🧭 Reference Trajectory

The desired path is generated as a circular trajectory:

```matlab
a_m = 3;
dt = 1/1e3;
StopTime = 10;
t = (0:dt:StopTime-dt);

X_ref = a_m * cos(pi/16 * t);
Y_ref = -a_m * sin(pi/16 * t);

path = [X_ref; Y_ref];
```

This trajectory is used as the reference input for evaluating the robot's tracking performance.

---

## 👁️ Observer Design

The project includes both **full-order** and **reduced-order** observer designs.

### Full-Order Observer

```matlab
L = place(A', C', [-20, -20, -100]);
L = L';
```

The full-order observer estimates all robot states from the available measured outputs.

### Reduced-Order Observer

```matlab
F = -40;
L_R = [1 -400];
T = lyap(-F, A, -L_R*C);
Q = inv([1 0 0; 0 1 0; T]);
```

The reduced-order observer estimates only the unavailable part of the state vector, which can reduce complexity while maintaining useful estimation performance.

---

## 📊 Simulation Results

The repository contains result figures showing the behavior of the upgraded system and observer-based simulations.

### Upgraded System

<p align="center">
  <img src="figures/upgradedSys.PNG" alt="Upgraded System" width="700">
</p>

### Full-Order Observer on Upgraded System

<p align="center">
  <img src="figures/fullOrderObserver-upgradSys.PNG" alt="Full Order Observer" width="700">
</p>

### Reduced-Order Observer on Upgraded System

<p align="center">
  <img src="figures/reducedOrderObserver-upgradeSys.PNG" alt="Reduced Order Observer" width="700">
</p>

---

## 📈 Main Project Phases

### Phase 1 — Modeling

The robot model is formulated in state-space form and prepared for controller design.

### Phase 2 — Feedback Control

A feedback controller is designed to stabilize the robot and achieve desired closed-loop dynamics.

### Phase 3 — Integral Action

Integral states are added to improve trajectory tracking and reduce steady-state error.

### Phase 4 — Observer-Based Control

Full-order and reduced-order observers are implemented to estimate robot states and test performance on the upgraded system.

---

## ✅ Features

- Differential-drive mobile robot modeling
- MATLAB-based controller implementation
- Simulink simulation models
- State feedback controller design
- Integral controller design
- Full-order observer design
- Reduced-order observer design
- Circular trajectory generation
- Upgraded system analysis
- Final report and presentation included

---

## 📚 Learning Outcomes

By studying this project, you can learn how to:

- Represent mobile robot dynamics using state-space models.
- Design stable feedback controllers using pole placement.
- Add integral control for better tracking performance.
- Build state observers for robotic systems.
- Compare full-order and reduced-order observer behavior.
- Simulate mobile robot control systems in MATLAB/Simulink.

---

## 📄 Documentation

Additional explanation and project details are available in:

- `Report_final.pdf`
- `Modern_Presentation_Final.pptx`
- `LS_phase1_2.mlx`

---

## 👤 Author

**Mohammad Barabadi**  
GitHub: [@mohammadbrd](https://github.com/mohammadbrd)

---

<div align="center">

### 🤖 Designed for learning, simulating, and analyzing modern mobile robot control systems.

</div>

<div align="center">

### ⭐ If you find this project useful, consider starring the repository.

</div>
