# Damped Driven Pendulum
A classical system which upon displacement from equilibrium position experiences a restoring force proportional to the displacement is termed as the harmonic oscillator. 
Mathematically, an ideal oscillator is described as,

$$F = -kx$$

Any mass subject to a force in a state of stable equilibrium acts as a harmonic oscillator for small vibrations.
The significance of harmonic oscillators lies in their abundance in natural systems and their exploitaion in many devices.

If only a restoring force is acting on the system, it is said to undergo simple harmonic motion and is called a simple harmonic oscillator. It undergoes oscillations with constant amplitude and frequency independant of each other while the equilibrium point is fixed.

In the presence of other damping forces proportional to the velocity, the system is a damped oscillator.[^1] The system either oscillates with a frequency lower than the undamped system and an amplitude decreasing with time (underdamped) or decay to the equilibrium position without any significant oscillations (overdamped). The situation depends on the friction coefficient,
Consider the frictional force is linear then,

$$F_{T} = F_{spring} + F_{frictional}$$

$$F_{T} = -kx - bv$$ 
where b = friction coefficient or viscous damping coefficient

Driven oscillators are damped harmonic oscillators that are affected by a time dependant externally applied force F(t).

In this case Newton's Law takes the form,

$$F = F_{spring} + F_{viscous} + F_{driving}$$

Let the driving force is periodic with a constant amplitude,

$$F = -kx -bv +F_{0} cos(wt)$$

$$m\ddot{x} + b\dot{x} + k x = F_{0}cos(\omega) t$$

Dividing both sides by m and using $\gamma = \frac{b}{m}, \omega_{0}^{2} = \frac{k}{m}$, to get the standard form,

$$\ddot{x} + \gamma \dot{x} + \omega_{0}^{2} x = \frac{F_{0}}{m} cos(\omega t)$$ [^2]

The general solution is a sum of a transient solutions that depends on initial conditions, and a steady state that is independent of initial conditions and depends only on the driving amplitude $$F_{0}$$, driving frequency $$\omega$$, undamped angular frequency $$\omega_{0}$$, and the damping ratio $$\zeta =\frac{F_{0}}{mg}$$.[^4]

The driving force $$\zeta = \frac{F_{0}}{mg}$$ is the dimensionless drive ratio. For a small oscillator, large amplitudes can't be achieved and it is observed that after a transient period the system settles to the driving frequency.Thus, the initial behaviour of the system depends on the initial conditions but any differences due to initial conditions decay rapidly.

However, when the driving force is comparable to the weight, complicated non-linear behaviours arise. In other words, increasing the value $$\zeta$$ leads to large scale motion.

## Period Doubling and Bifurcation point
For different values of $$\zeta>1$$, the initial oscillations are wild. For instance, at $$\zeta = 1.06$$, a pendulum swings from $$\phi = 0$$ to $$\phi = 5\pi$$ in the first three drive cycles and undergoes two more cycles before settling down to quasi-sinusoidal oscillations. At $$\zeta = 1.073$$, it undergoes 20 unruly drive cycles and then settles to an oscillation motion with double the original period.[^5] This phenomena is known as period doubling. At a specific point, the one-cycle (single repeating state) undergoes a bifurcation, leading to a two-cyle state. A new periodic trajectory emerges with twice the period of the original. Further increase in the drive strength can lead to further bifurcation points and consequently increased period of motion.












