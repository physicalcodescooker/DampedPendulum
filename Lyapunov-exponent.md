## Solving the oscillation equation of motion
We implement the driven damped pendulum oscillation equation. 
$d²θ/dt² + (1/q)(dθ/dt) + sin(θ) = g·cos(ω_d·t)$
Here,
dθ/dt = ω: Kinematic relation (definition of angular velocity)

-(1/q)ω: Viscous damping (energy dissipation)

-sin(θ): Gravitational restoring torque (the term that is non-linear.)

g·cos(ω_d·t): External periodic forcing (energy input)

The solution is provided using the odient function.
```python
def pend(y, t, q, g, omega_d):
    theta, omega = y
    dtheta_dt = omega
    domega_dt = -(1/q) * omega - np.sin(theta) + g * np.cos(omega_d * t)
    return [dtheta_dt, domega_dt]
```

```python
def poincare_section(q, g, omega_d, y0, n_periods=500, transient_periods=100):
    # Period of driving force
    T = 2 * np.pi / omega_d
    
    # Total time
    total_periods = transient_periods + n_periods
    t_span = np.linspace(0, total_periods * T, total_periods * 50)
    
    # Solve ODE
    sol = odeint(pend, y0, t_span, args=(q, g, omega_d))
    
  
    # Skip transient periods
    sample_indices = np.arange(transient_periods * 50, len(t_span), 50)
    
    theta_poincare = sol[sample_indices, 0]
    omega_poincare = sol[sample_indices, 1]
    
    # Wrap theta to [-pi, pi] for better visualization
    theta_poincare = np.mod(theta_poincare + np.pi, 2*np.pi) - np.pi
    
    return theta_poincare, omega_poincare
```
