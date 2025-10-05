As a warmup, I first analyse the behaviour of the trajectory of the harmonic ocsillator using the non-linear second order differential equation of motion,

  $\frac{d^{2}}{d\theta^{2}} + \frac{1}{q} \frac{d\theta}{dt} +sin(\theta) = gcos(\omega_{D})$      (1)

where $\omega_{D}$ is the driving frequency that is provided by an external force on a damped oscillator. The damping of the oscillator is due to a force that is proportional to the velocity (frictional force) and thus the damping term in (1) is  $\frac{1}{q} \frac{d\theta}{dt}$. 

By taking the driving term as a constant independant of time, there are two ordinar differential equations (1) can be converted into,

 $\frac{d\theta}{dt} = \omega$                           (2)
 
  $\frac{d\omega}{dt} = -\frac{1}{q}\omega - sin\theta + gcos(\omega_{D}t)$ (3)

Equation (3) is non-linear and so is expected to exhibit chaotic motion for particular values of q, g and $\omega_{D}$. 

Modelling this system in Python is carried out using the 'odeint' function to solve the differential equations (2) and (3). 
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

def pend(y, t, q, g, omega_d):
    theta, omega = y
    
    dtheta_dt = omega
    domega_dt = -(1/q) * omega - np.sin(theta) + g * np.cos(omega_d * t)
    
    return [dtheta_dt, domega_dt]

# Parameter
q = 2.0          # Quality factor (damping)
g = 0.9          # Driving amplitude
omega_d = np.pi  # Driving frequency

# Time array
t = np.linspace(0, 50, 1000)

# Initial conditions: [theta_0, omega_0]
y0 = [np.pi - 0.1, 0]

# Solve ODE
sol = odeint(pend, y0, t, args=(q, g, omega_d
))

# Extract solutions
theta_sol = sol[:, 0]
omega_sol = sol[:, 1]
```
The variables theta_sol and omega_sol are lists containing different values of $\theta$ and $\omega$ respectively for the time interval [0,50]. Visualization of solution is done using matplotlib. First $\theta$ is plotted against time to show how the oscillation is affected by the damping and the driving force with time.
```python
# Create plots
fig, (ax1,ax2) = plt.subplots(2,1, figsize=(10, 8))

# Plot theta vs time
ax1.plot(t, theta_sol, 'b-', linewidth=1)
ax1.set_xlabel('Time')
ax1.set_ylabel('θ (radians)')
ax1.set_title('Driven Damped Pendulum: Angle vs Time')
ax1.grid(True, alpha=0.3)

# Plot phase space (theta vs omega)
ax2.plot(theta_sol, omega_sol, 'r-', linewidth=0.5, alpha=0.7)
ax2.set_xlabel('θ (radians)')
ax2.set_ylabel('ω (angular velocity)')
ax2.set_title('Phase Space')
ax2.grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
```
<img width="989" height="790" alt="download" src="https://github.com/user-attachments/assets/cc04b1b8-d59a-475a-8622-cded80bf4604" />


The driven damped pendulum starting near the initial position exhibits a 16-second transient phase before settling into steady-state periodic motion. 
Starting from θ ≈ π with zero velocity, the pendulum undergoes large-amplitude oscillations (t = 0-16s) as damping dissipates initial gravitational potential energy. 
During this transitioning period, the driving force gradually establishes phase coherence or a stable frequency to match that of the pendulum motion.

After t ≈ 16s, the system reaches dynamical equilibrium, settling into small-amplitude periodic oscillations (θ ≈ 0 ± 0.1 rad) centered at vertical equilibrium. 
This steady state represents a limit cycle attractor where energy input from driving exactly balances energy loss from damping.


### Phase Space Interpretation
The phase space trajectory reveals the system's dissipative nature through its inward spiral pattern. This curve demonstrates how the system tends to move toward the limit cycle, with the spiral spacing decreasing as the change in the frequency decays and it moves towards stability. 
The closed orbit in steady state confirms periodic behavior, characteristic of the sub-chaotic regime (g < 0.7).
