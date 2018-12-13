---
layout: page
title: "How the Car Handles (Ground)"
---

## Problem Statement

When driving a car, the user can specify throttle (positive or negative),
steering, and boost. For now, we will not consider the effects of
powersliding. We are interested in predicting how the car
will respond to these inputs, given its current velocity $$ \boldsymbol{v}$$,
angular velocity $$\boldsymbol{\omega}$$, and orientation matrix $$\boldsymbol{\Theta}$$.

### Motion in the Plane 

If the car is on the ground, we can characterize its
position and orientation with only 3 numbers:
an $$x$$ and $$y$$ coordinate for where it is in
the plane, and an angle $$\theta$$ that describes
the direction the car is facing.

To predict the car's motion, we need to develop
a model for the two in-plane forces, and the torque
normal to the surface. Let us denote these force components by
$$F_f$$ and $$F_\ell$$ 
(with subscripts indicating the force in the $$f$$orward and $$\ell$$eft
directions, respectively) and let the torque be $$\tau$$.

### Turning

Consider what happens when we steer all the way to the left
and increase the car's throttle:

<video autoplay loop muted width="640">
<source type="video/webm" src="/videos/turning_radius.webm">
Your browser does not support the video element.
</video>

If we look closely, we can see that the front wheels change direction
as we accelerate (steering is kept constant). Specifically, the wheels
tend to straighten out as the car's speed increases. This means that the
car turns more tightly when it is moving slowly (or, that the turning
radius gets bigger as it speeds up). 

To quantify this effect, the car's steering was set to maximum, and
the curvature of its trajectory ($$\kappa \propto \frac{1}{r}$$) was 
logged along with its velocity. The data points are shown below:

![](/images/RocketLeague/turning_curvature.png)

From this, we see that the curvature seems to vary in a piecewise linear
way with respect to velocity. We can fit a function to this data (shown
in red), and use it to predict rates of turning:

![](/images/RocketLeague/turning_curvature_with_fit.png)

Running a similar tests with different values of steering shows that the 
maximum angular velocity for a given speed is roughly proportional to the
input steering. From here, we define the torque to be ($$s$$ is the user-input
steering, between -1 and 1):

$$ \tau \;\; \propto \;\; s \; \kappa(|v_f|) \; v_f \; - \; \omega_u $$

The first term can be understood as the target angular velocity, $$\omega_t$$. If
the car is already turning with $$\omega_u = \omega_t$$, then the torque is zero, and
nothing changes. If the user changes the steering, the target angular velocity changes,
and the actual angular velocity will try to follow it.

### Accelerating

The time rate of the car's forward velocity ($$v_f$$) seems to be broken up in to a handful of
separate cases. In no particular order:

#### Braking

If the sign of the car's forward velocity is opposite from the input throttle, then
the car experiences a very large, constant braking force, $$B$$.

$$ F_f = -F_{\text{br}} \; \text{sgn}(v_f) $$

Note: this is also true when boosting while moving backwards

#### Boosting (Slow)

When the car is moving slowly ($$v_f < v_{\text{thr}} \approx 1400$$), boost accelerates the car in the following way:

$$ F_f = v_{\text{max}} - v_f $$

#### Boosting (Fast)

When the car is moving quickly ($$v_f > v_{\text{thr}}$$), boost gives the car a constant acceleration,
until it reaches $$v_{\max} \approx 2300$$:

$$ F_f = \begin{cases}
  F_{\text{boost}} & \; v_{\text{thr}} \leq v_f < v_{\max} \\
  0 & \; v_{\max} \leq v_f
\end{cases}$$

#### Coasting

If the car is not boosting and has nearly zero throttle, it will tend to slow down but more slowly
than braking:

$$ F_f = -F_{c} \; \text{sgn}(v_f) $$

#### Throttle

If the car is not boosting, but has nonzero throttle, its motion is described by
($$T$$ is the user-input throttle, between -1 and 1):

$$ F_f = T \; (F_{\text{thr}} - |v_f|) $$


### Empirical Models

There are some uglier parts of this model that include damping
from turning and the expression of $$F_\ell$$, which have been 
determined just through empirical curve fitting of game data. 
These are not so easily described, but a simple implementation 
is [available](https://github.com/samuelpmish/Lobot/blob/master/src/Car.cpp). 
I expect to update these expressions in the future,
to improve simulation accuracy.

## Example Predictions

These plots compare actual car trajectories recorded in Rocket
League (solid lines) to the predicted trajectories computed with
this model of driving physics, given only the initial conditions
(dashed lines). These plots are generated from data file 
"episode\_00.csv" in the dataset provided 
[here](https://github.com/samuelpmish/Lobot/tree/master/assets/car_control/ground_driving_no_handbrake)


Car positions, as a function of time step:
![](/images/RocketLeague/driving_positions_0.png)

Car velocities, as a function of time step:
![](/images/RocketLeague/driving_velocities_0.png)

Car angular velocities, as a function of time step:
![](/images/RocketLeague/driving_angular_velocities_0.png)


Here, the uncertainties can accumulate relatively quickly.
These episodes are stress-tests that include many abrupt
changes in steering and throttle. The values after 5 seconds
of simulation are reasonable approximations of the actual data, 
but have noticeable error.

## Notes and Caveats

Right now, my models treat driving forward and driving backward
in a symmetric way. However, it seems to be the case
that driving backwards is actually subtly different. The parameters
are tuned to be most accurate for driving forward, so errors are
more pronounced for trajectories where the car spends most of its
time going backwards.

Also, I am working to see if I can get the simulation to take
the field geometry into account so that one might be able to predict
paths that involve driving on the ground and the walls.
