# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program - Model Predictive Control (MPC) Project

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./mpc`.

## Rubric points
### The Model
The model used is a Kinematic model neglecting the complex interactions between the tires and the road. The overall equations look like below:  
<img src="image/mpc.JPG" width="800">  

The state vector is comprised of: 
* vehicle's x
* vehicle's y 
* orientation angle (psi) 
* velocity (v), 
* cross-track error (cte) - the distance we want to minimize, between predicted and the trajectory
* psi error (epsi) - the angle we want to minimize, between the vehicle orientation and trajectory orientation  

In this model, the Actuator is comprised of acceleration (a) and steering angle (delta). 

### Timestep Length and Elapsed Duration (N & dt)
N is the number of timesteps in the horizon. dt is how much time elapses between actuations. The values chosen for N and dt are 10 and 0.1. These values mean that the optimizer is considering a one-second duration in which to determine a corrective trajectory.   
A general guidelines introduced in the course: T should be as large as possible, while dt should be as small as possible. but there is tradeoff. 
* Why smaller dt is better?   
smaller dt means finer resolution. Larger values of dt result in less frequent actuations, which makes it harder to accurately approximate a continuous reference trajectory
* Why larger N isn't always better?   
If set N a large number, the simulation would run much slower  

I have tried other values: 20 / 0.05 and 5 / 0.2, but the car moved out of track very soon…

### Polynomial Fitting and MPC Preprocessing
A 3rd-degree polynomial is fitted to the transformed waypoints, because it is known to fit most of the roads. Using a smaller order can result in underfitting while using a higher order can result in overfitting.
In this version I have simplified the code in main.cpp (from line 106)

### Model Predictive Control with Latency
Dealing with latency in this updated version was referenced by an good idea from the website, that is: 
Since dt has been set to 0.1 (100ms), this interval happens to be the same value of latency. There are three lines of code in MPC.cpp to handing this (from line 115). 


This project was also run in Udacity workspace    
<img src="image/simulator.JPG" width="800">  
