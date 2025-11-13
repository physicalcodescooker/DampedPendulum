# Damped Driven Pendulum
A classical system which upon displacement from equilibrium position experiences a restoring force proportional to the displacement is termed as the harmonic oscillator. 
Mathematically, an ideal oscillator is described as,

$$F = -kx$$

Any mass subject to a force in a state of stable equilibrium acts as a harmonic oscillator for small vibrations.
The significance of harmonic oscillators lies in their abundance in natural systems and their exploitaion in many devices.

If only a restoring force is acting on the system, it is said to undergo simple harmonic motion and is called a simple harmonic oscillator. It undergoes oscillations with constant amplitude and frequency independant of each other while the equilibrium point is fixed.

In the presence of other damping forces proportional to the velocity, the system is a damped oscillator. The system either oscillates with a frequency lower than the undamped system and an amplitude decreasing with time (underdamped) or decay to the equilibrium position without any significant oscillations (overdamped). The situation depends on the friction coefficient,
Consider the frictional force is linear then,

$$F_{T} = F_{spring} + F_{frictional}$$

$$F_{T} = -kx - bv$$ 
where b = friction coefficient or viscous damping coefficient

Driven oscillators[^1] are damped harmonic oscillators that are affected by a time dependant externally applied force F(t).

In this case Newton's Law takes the form,

$$F = F_{spring} + F_{viscous} + F_{driving}$$

Let the driving force is periodic with a constant amplitude,

$$F = -kx -bv +F_{0} cos(wt)$$

$$m\ddot{x} + b\dot{x} + k x = F_{0}cos(\omega) t$$

Dividing both sides by m and using $\gamma = \frac{b}{m}, \omega_{0}^{2} = \frac{k}{m}$, to get the standard form,

$$\ddot{x} + \gamma \dot{x} + \omega_{0}^{2} x = \frac{F_{0}}{m} cos(\omega t)$$ [^2]

The general solution is a sum of a transient solutions that depends on initial conditions, and a steady state that is independent of initial conditions and depends only on the driving amplitude $$F_{0}$$, driving frequency $$\omega$$, undamped angular frequency $$\omega_{0}$$, and the damping ratio $$\zeta =\frac{F_{0}}{mg}$$.[^3]

The driving force $$\zeta = \frac{F_{0}}{mg}$$ is the dimensionless drive ratio. For a small oscillator, large amplitudes can't be achieved and it is observed that after a transient period the system settles to the driving frequency.Thus, the initial behaviour of the system depends on the initial conditions but any differences due to initial conditions decay rapidly.

<p float='left'>
<img width="495" height="395" alt="download" src="https://github.com/user-attachments/assets/2cd300b9-ee61-47e9-8ef4-27e11c2523fe">
<img width="495" height="395" alt="download" src="https://github.com/user-attachments/assets/9ea4e0c4-88d4-40c8-8283-2915a5983255" />
</p><p><em>  The oscillations at small values of the drive ratio while the phase space shows how the system stabilizes despite initial conditions.</em></p>

<p float='left'>
<img width="495" height="395" alt="download" src="https://github.com/user-attachments/assets/9bca9b1b-1a30-4ccf-aa47-c572f499a68e" />
<img width="495" height="395" alt="download" src="https://github.com/user-attachments/assets/fb0ca360-0afc-4fdb-96bf-667051202e32" />
</p><p><em> An instance of different initial conditions.</em></p>

However, when the driving force is comparable to the weight, complicated non-linear behaviours arise. In other words, increasing the value $$\zeta$$ leads to large scale motion.

## Period Doubling and Bifurcation point
For different values of $$\zeta>1$$, the initial oscillations are wild. For instance, at $$\zeta = 1.06$$, a pendulum swings from $$\phi = 0$$ to $$\phi = 5\pi$$ in the first three drive cycles and undergoes two more cycles before settling down to quasi-sinusoidal oscillations. At $$\zeta = 1.073$$, it undergoes 20 unruly drive cycles and then settles to an oscillation motion with double the original period.[^3] This phenomena is known as period doubling[^5]. At a specific point, the one-cycle (single repeating state) undergoes a bifurcation, leading to a two-cyle state. A new periodic trajectory emerges with twice the period of the original. Further increase in the drive strength can lead to further bifurcation points and consequently increased period of motion.


## Route to Chaos
With the gradual increase in the driving strength, the period of the motion continues doubling. At $$\zeta_{c} =1.0829$$, known as the critical value, the DDP starts behaving chaotically. At this stage, the pendulum exhibits erratic motion that seems to be struggling to oscillate with the period of the driver. The oscillations never repeat themselves exactly, as the trajectry of phase space spirals around without any closed loops.
Comparing the simulations



### Refrences
[1] LibreTexts. (2016, October 18). 15.6: Damped Oscillations. Physics LibreTexts. https://phys.libretexts.org/Bookshelves/University_Physics/University_Physics_(OpenStax)/Book%3A_University_Physics_I__Mechanics_Sound_Oscillations_and_Waves_(OpenStax)/15%3A_Oscillations/15.06%3A_Damped_Oscillations

[2],[4] Borkar, V. (2015). Oscillations in Damped Driven Pendulum: A Chaotic System. International Journal of Scientific and Innovative Mathematical Research (IJSIMR), 3(10), 14–27. https://www.arcjournals.org/pdfs/ijsimr/v3-i10/5.pdf

[3] Taylor, J. R. (2004). Classical Mechanics. University Science Books.

[5] Wikipedia contributors. (2025, October 4). Period-doubling bifurcation. In Wikipedia, The Free Encyclopedia. Retrieved 12:29, November 13, 2025, from https://en.wikipedia.org/w/index.php?title=Period-doubling_bifurcation&oldid=1315027005






