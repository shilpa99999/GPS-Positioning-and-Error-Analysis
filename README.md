# GPS-Positioning-and-Error-Analysis

### **Project Overview: GPS Positioning and Error Analysis**

The project focuses on solving the **GPS positioning problem**, which involves determining the precise location (x, y, z) of a GPS receiver and correcting for time drift \(d\) between the receiver and satellite clocks. GPS relies on signals transmitted from at least four satellites to calculate the receiver's position. This project investigates the mathematical formulation, numerical methods, and sensitivity of the GPS problem to errors in satellite transmission times.


### **Project Objective**
1. Solve the system of nonlinear equations arising in GPS positioning to determine the receiver's position \((x, y, z)\) and time correction \(d\).
2. Analyze the **conditioning** of the GPS problem to assess its sensitivity to small errors in satellite transmission times.
3. Compare error magnification factors and condition numbers for different satellite configurations, including tightly grouped and widely spaced satellites.


### **Key Components of the Project**

#### **1. GPS Fundamentals**
- GPS uses 24 specialized satellites, synchronized atomic clocks, and precise tracking to determine the receiver's position on Earth.
- The receiver monitors signals from at least four satellites, calculates distances based on signal travel time, and solves nonlinear equations to locate its position.

#### **2. Mathematical Formulation**
- The receiver's position \((x, y, z)\) lies at the intersection of four spheres with known centers \((A_i, B_i, C_i)\) and radii proportional to signal travel times \(t_i\):  
  \[
  \sqrt{(x - A_i)^2 + (y - B_i)^2 + (z - C_i)^2} = c(t_i - d)
  \]  
  where \(c\) is the speed of light. These equations account for the time drift \(d\) in the receiver's clock.

#### **3. Numerical Solution of Nonlinear Equations**
- Use **Multivariate Newton's Method** to iteratively solve the nonlinear system for \((x, y, z, d)\) with an initial guess of \((0, 0, 6370, 0)\).
- Analyze the system's sensitivity to input errors and assess its numerical conditioning.

### **Tasks Performed**

#### **Task 1: Solve for Receiver Position and Time Correction**
- Implement Multivariate Newton's Method to solve the system for the given satellite positions:
  \[
  (A_i, B_i, C_i) = (15600, 7540, 20140), (18760, 2750, 18610), (17610, 14630, 13480), (19170, 610, 18390)
  \]
  and measured time intervals:
  \[
  t_i = 0.07074, 0.07220, 0.07690, 0.07242 \, \text{sec}.
  \]
- Use the initial guess \((x_0, y_0, z_0, d_0) = (0, 0, 6370, 0)\).
- Compute the receiver's position \((x, y, z)\) and time drift \(d\).

#### **Task 2: Analyze Conditioning of the GPS Problem**
- Define satellite positions in spherical coordinates:
  \[
  A_i = \rho \cos(\phi_i) \cos(\theta_i), \, B_i = \rho \cos(\phi_i) \sin(\theta_i), \, C_i = \rho \sin(\phi_i),
  \]
  where \(\rho = 26570 \, \text{km}\), \(0 \leq \phi_i \leq \pi/2\), and \(0 \leq \theta_i \leq 2\pi\).
- Set \((x, y, z, d) = (0, 0, 6370, 0.0001)\) and calculate ranges \(R_i\) and travel times \(t_i\).
- Introduce a backward input error \(\Delta t_i = \pm 10^{-8}\), corresponding to a 3-meter positional error at the speed of light.
- Compute the forward error \(\|\Delta (x, y, z)\|_\infty\) and the error magnification factor:
  \[
  \text{Error Magnification Factor} = \frac{\|\Delta (x, y, z)\|_\infty}{c \|\Delta t_i\|_\infty}.
  \]
- Estimate the condition number of the problem based on the maximum error magnification factor.

#### **Task 3: Evaluate the Effect of Satellite Configuration**
- Compare the conditioning of the GPS problem for:
  - Loosely spaced satellites: Arbitrary values for \(\phi_i\) and \(\theta_i\).
  - Tightly grouped satellites: \(\phi_i\) and \(\theta_i\) within 5% of one another.
- Solve for the receiver's position with and without input errors.
- Analyze the impact of satellite grouping on error magnification factors and maximum positional errors.

### **Summary of Results**
1. **Receiver Position and Time Drift**:
   - Computed \((x, y, z)\) and \(d\) using Multivariate Newton's Method with the given satellite positions and time intervals.

2. **Conditioning Analysis**:
   - Quantified the sensitivity of the GPS system to small input errors in transmission times.
   - Calculated the condition number and error magnification factor for the loosely and tightly spaced satellite configurations.

3. **Effect of Satellite Grouping**:
   - Tightly grouped satellites showed increased sensitivity (higher error magnification) compared to loosely spaced satellites.
   - Provided insights into the impact of satellite geometry on GPS accuracy.

This project illustrates the challenges of solving ill-conditioned systems in GPS applications and highlights the importance of numerical methods in engineering and real-world problem-solving.
