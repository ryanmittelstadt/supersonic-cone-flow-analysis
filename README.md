# Technical Walk-through: Supersonic Conical Flow Simulation

## 1. Description

I chose this project to move beyond the 2D simplifications of oblique shock theory and explore the 3D complexities of conical flow. In supersonic flight, the flow field behind a conical shock is significantly different from that of a wedge, as the streamlines must compress further to follow the body's surface. My goal was to utilize numerical integration to understand how local flow properties—like Mach number and thermodynamic ratios—adjust between the shock wave and the cone surface.
<br />

* **The Problem:** Simulate supersonic flow at Mach 5 past a cone with a $12^{\circ}$ shock wave angle.
* **The Methodology:** Solve the nonlinear Taylor-Maccoll equation using a fourth-order Runge-Kutta (RK4) numerical method.

## 2. Mathematical Methodology & Initial Conditions

The project assumes steady, axisymmetric, and inviscid flow. The physics are governed by the Taylor-Maccoll equation, which I reduced from a second-order ODE into a system of two first-order ODEs to facilitate numerical integration.

### Defining the State Variables
The state is defined by the velocity components relative to the cone axis:
<br />

* **$V_r$:** Radial velocity component.
* **$V_{\theta}$:** Tangential velocity component.

### Boundary Conditions
The simulation begins at the shock wave ($\theta_s = 12^{\circ}$) and integrates inward toward the cone surface.
<br />

* **Initial Condition:** Post-shock velocity components are calculated using standard normal shock relations and flow deflection angles.
* **Terminating Condition:** The simulation concludes at the cone surface ($\theta_c$), where the tangential velocity $V_{\theta}$ must logically be zero to satisfy the flow-tangency condition.

## 3. MATLAB Implementation: The RK4 Solver

I implemented the fourth-order Runge-Kutta method in MATLAB to navigate the strong nonlinearities of the flow equations.
<br />

* **Step Size:** A small marching step size ($\Delta\theta = -0.1^{\circ}$) was used to ensure high precision and stability.
* **Iterative Process:** At each step, the solver recomputes the velocity magnitude, local Mach number, and thermodynamic ratios ($P/P_1, T/T_1, \rho/\rho_1$) based on isentropic relations.
* **Validation:** Final values at the cone surface were cross-checked against NACA Report 1135 (Charts 5, 6, and 7), confirming the accuracy of my numerical results.

## 4. Results & Aerodynamic Discussion

The simulation provided a detailed profile of the conical flow region, showing a smooth transition from post-shock conditions to the cone surface.

<p align="center">
  <img src="https://i.imgur.com/G6IYz0R.png" height="80%" width="80%" alt="Tangential Velocity vs Theta"/>
  <br />
  <i>Figure 6.0-1: Tangential Velocity ($V_{\theta}/V_{max}$) vs. $\theta$</i>
</p>

**Observation:** This plot shows the tangential velocity decaying toward zero as it approaches the cone surface, satisfying the physical boundary condition.

<p align="center">
  <img src="https://i.imgur.com/nLbxVXR.png" height="80%" width="80%" alt="Mach Number vs Theta"/>
  <br />
  <i>Figure 7.0-1: Mach Number vs. $\theta$</i>
</p>

**Observation:** The Mach number decreases smoothly as the flow compresses behind the shock.

<p align="center">
  <img src="https://i.imgur.com/bp5xBXM.png" height="80%" width="80%" alt="Thermodynamic Ratios vs Theta"/>
  <br />
  <i>Figure 8.0-1: Thermodynamic Ratios vs. $\theta$</i>
</p>

**Observation:** Pressure ($P_c/P_1$), Temperature ($T_c/T_1$), and Density ($\rho_c/\rho_1$) ratios all rise progressively as the flow moves toward the cone surface.

### Final Surface Properties
At the cone surface, the simulation converged on:
<br />

* **Surface Mach Number ($M_c$):** $\approx 4.77$
* **Pressure Ratio ($P_c/P_1$):** $\approx 1.31$
