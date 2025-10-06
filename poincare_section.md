## Solving the oscillation equation of motion
We implement the driven damped pendulum oscillation equation. 
$d²θ/dt² + (1/q)(dθ/dt) + sin(θ) = g·cos(ω_d·t)$
Here,

$dθ/dt = ω$ : Kinematic relation (definition of angular velocity)

$-(1/q)ω$ : Viscous damping (energy dissipation)

$-sin(θ)$ : Gravitational restoring torque (the term that is non-linear.)

$g·cos(ω_d·t)$ : External periodic forcing (energy input)

```python
def pend(y, t, q, g, omega_d):
    theta, omega = y
    dtheta_dt = omega
    domega_dt = -(1/q) * omega - np.sin(theta) + g * np.cos(omega_d * t)
    return [dtheta_dt, domega_dt]
```
## Poincare Map
In dynamical systems, a poincare map or a poincare section is a one dimension lower subspace of the phase space that is often used for analyzing the original system in a simpler way. It is like the cross-section of the phase space that shows a transversal flow of the state of system. Transversal means that the system's trajectories cross this surface rather than moving parallel to it. The map is discrete instead of continuos.

If there is a single fixed point that the trajectory passes through after completing an orbit than the motion is periodic and exhibits stability. Such a system is not chaotic and executes identical motion each cycle.

If there a set of fixed points that form a closed curve usually reflect a quasi-periodic behaviour. 

If the points on the poincare section are scattered in a random order with no closed loops or a distinct coherent pattern than the motion exhibited by the system is purely chaotic. The motion stays ina bounded region around the fractal attractor and the trajectory is dense.

The driven damped pendulum is a 3D dynamical system of angle, position and time due to the time-dependant driving force. To visualize the 3D chaos, a 2D poincare section is constructed. The poincare section shows the transversal trajectory at fixed periods of time and so the time dimension is dropped.
```python
def poincare_section(q, g, omega_d, y0, n_periods=500, transient_periods=100):
    # Period of driving force
    T = 2 * np.pi / omega_d
    
    # Total time
    total_periods = transient_periods + n_periods #Number of driving period
    t_span = np.linspace(0, total_periods * T, total_periods * 50) 
    
    # Solve ODE
    sol = odeint(pend, y0, t_span, args=(q, g, omega_d))
    
  
    # Skip transient periods
    sample_indices = np.arange(transient_periods * 50, len(t_span), 50)
    
    theta_poincare = sol[sample_indices, 0]
    omega_poincare = sol[sample_indices, 1]
    
    # Wrap theta to [-pi, pi] for better visualization
    theta_poincare = np.mod(theta_poincare + np.pi, 2*np.pi) - np.pi # Shifts and scales the values of theta between [0,2$\pi$] and then between [$\pi,-\pi$] to make the visualization more appealling 
    
    return theta_poincare, omega_poincare
```

The points on the section appear at a period of $$T = \frac{2\pi}{w_{d}}$$. 

After solving the ODE uisng the odient function, the 'sol' variable contains the complete trajectory of the phase space. The solution contains a set of arrays with the values of $\theta$, $\omega$ and t respectively. From this array the sample points or the points to be plotted on the poincare section are extracted. 

The 'sample_indices' variable skips the periods in the transient decay so that the system settles onto the attractor and forgoes the initial conditions and takes points that are at the same phase of the driving force (e.g 50T, 51T, etc). The variables 'theta_poincare' and 'omega_poincare'  extract values of $\theta$ and $\omega$ at sample points respectively.
 ##Plotting the Phase Space and Poincare section
 ```python
 # Chaotic parameters
q = 2
g = 1.5
omega_d = 2/3

# Create figure with multiple subplots
fig = plt.figure(figsize=(16, 10))

# 1. Full phase space trajectory
t_full = np.linspace(0, 200, 10000)
y0 = [0.1, 0]
sol_full = odeint(pend, y0, t_full, args=(q, g, omega_d))

ax1 = plt.subplot(2, 3, 1)
ax1.plot(sol_full[5000:, 0], sol_full[5000:, 1], 'b-', linewidth=0.3, alpha=0.5)
ax1.set_xlabel('θ (rad)')
ax1.set_ylabel('ω (rad/s)')
ax1.set_title('Full Phase Space Trajectory\n(after transient)')
ax1.grid(True, alpha=0.3)

# 2. Poincaré section - single initial condition
theta_p, omega_p =poincare_section(q, g, omega_d, y0, n_periods=500)

ax2 = plt.subplot(2, 3, 2)
ax2.plot(theta_p, omega_p, 'r.', markersize=2, alpha=0.6)
ax2.set_xlabel('θ (rad)')
ax2.set_ylabel('ω (rad/s)')
ax2.set_title(f'Poincaré Section \nq={q}, g={g}, ω_d={omega_d:.3f}')
ax2.grid(True, alpha=0.3)
```
<img width="1619" height="876" alt="chaos 1" src="https://github.com/user-attachments/assets/b89b478e-5d12-43a2-b115-bf8a4116f69e" />

## Effect of increasing the time of integration or the temporal sampling
Increasing the sampling resolution or the number of points in the 't_span' array, reveals the intricate structure of the fractor attractor and provides a probabilistic distribution of the long term behaviour of the system.This also gives higher accuracy on the measurement of the sensitivity of the system to initial conditions.

### For   t_span = np.linspace(0, total_periods * T, total_periods * 100) 
<img width="1619" height="876" alt="chaos 2" src="https://github.com/user-attachments/assets/f37b942a-7f74-4b3d-ba8f-200bd67e5b64" />

### For  t_span = np.linspace(0, total_periods * T, total_periods * 500)
<img width="1232" height="876" alt="chaos3" src="https://github.com/user-attachments/assets/3d8bf660-4b69-4caa-b6ca-52123544d82e" />

### For  t_span = np.linspace(0, total_periods * T, total_periods * 1000)
<img width="1232" height="876" alt="chaos4" src="https://github.com/user-attachments/assets/55cbbbab-0389-4ee2-bc6e-3c234c92ed5d" />

### For  t_span = np.linspace(0, total_periods * T, total_periods * 5000)
<img width="1232" height="876" alt="choas 5" src="https://github.com/user-attachments/assets/5235e189-5c72-4e36-a854-2c1f5382c2b3" />

### For  t_span = np.linspace(0, total_periods * T, total_periods * 10000) (It just gets prettier, doesn't it?)
<img width="1232" height="876" alt="chaos 6" src="https://github.com/user-attachments/assets/f99553d7-a4f0-48b8-81f3-591e533e689a" />
