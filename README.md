# Damped Driven Pendulum
A comprehensive study on the damped driven pendulum or harmonic oscillator.
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
sol = odeint(pend, y0, t, args=(q, g, omega_d))

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
```
<img width="989" height="790" alt="download" src="https://github.com/user-attachments/assets/2942d4ba-4d32-4a13-8711-780678ac596c" />
Ignore the plot labelled phase space for now, we analyze the graph. Initially the oscillationa trajectory shows two small peaks when the initial velocity is zero. This appears to be due to the presence of the driving frequency. On the other hand, the drop in the normal sinusoidal wave at the bottom is due the damping force which decreases the amplitude by some factor that makes it less than the normal amplitude. After some time the driving frequency is balanced by the drag which is shown by the normal sinusoidal trajectory after t~16s. The final angle oscillate in a really small interval.



