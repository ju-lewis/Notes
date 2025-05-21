
# Effectors

At least 6 degrees of freedom are required to arbitrarily position an end-effector in 3D space


>[!Note] Non-holonomic Robots
>A car has more DOF (3) than controls (2), so it's *non-holonomic*
>- Cannot generally transition between two infinitesimally close configurations

# Perception
We do not see the world as it is

Occasionally, perceived reality breaks down:
- Hallucinations
- Optical illusions


## Uncertainty in Actions
Actions do not always have the exact outcome we anticipate (i.e. trying to drive a perfect square without perception)
- This is why perception is important
- Even with perfect starting knowledge this is a problem (infinitely accumulating error)


An action $A_t$ as time $t$


### Motion Model
Update state using its movements $v_1 \Delta t$ and $\omega_1 \Delta t$

### Sensor Model
Use observation $h(x_t)$ of landmark $x_i, y_i$

>[!Info]
>We assume Gaussian noise in motion predictions and sensor range measurements

**Particle filtering** is a common method for performing localisation under uncertain conditions
- Start with evenly distributed particles and update distribution based on movement through the space
