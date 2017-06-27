# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---
# The Model

The kinematic model for the vehicle in this project. The states for the model are: [x,y,ψ,v] where the positions are x and y, the yaw angle is ψ, and the speed is v. The actuators are [δ,a] which stand for the steering angle and the acceleration. The equation is descibed as follows:

```
x(​t+1) = x(t) + v(t)∗cos(ψ(t))∗dt
y(​t+1)​​ = y(​t) + v(t)∗sin(ψ(t)​​)∗dt
ψ(​t+1) = ψ(t) + v(t)/Lf ∗ δ ∗ dt
v(​t+1) = v(​t) + a(t) ∗ dt
```

# Timestep Length and Elapsed Duration (N & dt)
```
N = 15
dt = 0.05
```
`N=15` keeps the trajectory long enough into the future. `dt=0.05` provides higher precision concerning the delay of 100ms. I tried larger timestep length, but at the speed of 60mph `N=15` is a good fit.

# Polynomial Fitting and MPC Preprocessing

A 3rd order polynomial is chosen to fit the waypoints. The coordinate system was transformed to the car's coordinate system before the processing.

# Model Predictive Control with Latency

I use the solution from the solver at a t=0.1s delay to count the latency. A better approach could be transforming the vehicle location using the motion model.