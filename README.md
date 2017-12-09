# self-driving-car-Model-Predictive-Control
- [CarND Term 2 Model Predictive Control (MPC) Project](https://github.com/udacity/CarND-MPC-Project)
- **Two objectives of MPC project**:
   - Speed: should come as close as possible to the desired speed based on the cost function.
   - How well the result is fitting 6 waypoints?
   

[MPC_process]: ./assets/MPC_process.PNG
   
# MPC(Model Predictive Control)
**Model Predictive Control** makes the job of following a trajectory as an _optimization problem_. The solution to the optimization problem is to define a cost function, and calculate the optimal trajectory.  We have to constantly re-evaluate because our trajectory prediction changes over time. 

**MPC Process**:
1. MPC Preprocessing
2. Apply MPC
3. Return results (steering value & throttle)

![alt text][MPC_process]

## MPC Preprocessing
1. Coordinates transformation
2. Polynomial Fit
3. Calc CTE & EPSI
### Coordinates transformation
- Wayponits are given in Global Map Coordinates. We need to transform the waypoints from Map Coordinate to Car coordinate. This process makes the next step (Polynomial fit AND CTE & EPSI calc) easier.
- [This visualization](https://discussions.udacity.com/t/mpc-car-space-conversion-and-output-of-solve-intuition/249469/12) helps me understand the coordinate transformation.
### Polynomial Fit
Fit 3rd order polynomial based on given 6 waypoints.
 - We adapt [this Polyfit](https://github.com/JuliaMath/Polynomials.jl/blob/master/src/Polynomials.jl#L676-L716) code.

### Calculate CTE (Cross Track Error) and EPSI (Angle Error).
 - CTE = polyeval(coeffs, x) - y;  Where (x, y) is car's posion in car coordinates. 
 - EPSI = psi - atan(coeffs[1] + 2*px*coeffs[2] + 3*coeffs[3]*pow(px,2));
 
 
## MPC
**MPC Steps**:
1. Set up everything required for the MPC loop: 
   - Duration of trajectory T by choosing N and dt. [N=10, dt=0.02].
   - Define vehicle model [x,y,psi,v,cte,psi_error] and constraints such as actual limitations [delta, a]. 
   - Define the cost function. 
2. MPC Loop:
   - Pass current state to MPC
   - Optimization solver is called. The solver uses initial state, the model constraints and cost function to return a controls inputs that minimize the cost function. The solver is IPOPT.
   - Apply the first control inputs to the vehicle
   - Repeat the loop

 Latency: a delay occurred as the control command propagates through the system. PID Controller cannot deal with it. But MPC can solve this issue.






# Install, edit and run the code instructions
## Dependencies
- Follow [this instruction](https://github.com/udacity/CarND-MPC-Project).
- Follow [this instruction](https://github.com/udacity/CarND-MPC-Project/blob/master/install_Ipopt_CppAD.md) to install Ipopt and CppAD.
- Notes:
    - ```install_ipopt.sh``` would not work using /mnt/repo.. under Bash on Ubuntu WIN 10. You have to ```git clone``` the repo using Bash on Ubuntu WIN 10.
    - AND execute ```./install_ipopt.sh``` won't work. It gives an Makefile error. We have to add sudo in front like ```sudo ./install_ipopt.sh```.
    
```bash
# update
sudo apt-get update

# gfortran dependency
sudo apt-get install gfortran

# get unzip
sudo apt-get install unzip

# Ipopt: get, install, unzip
wget https://www.coin-or.org/download/source/Ipopt/Ipopt-3.12.7.zip && unzip Ipopt-3.12.7.zip && rm Ipopt-3.12.7.zip
./install_ipopt.sh

# CppAD
sudo apt-get install cppad

# Gnuplot
sudo apt-get install gnuplot

# python and matplotlib
sudo apt-get install python-matplotlib
sudo apt-get install python2.7-dev
```
    
## Edit the code
- use Visual Studio Code to edit the code in the WINDOWS environmnet.
- use /mnt/repo... to compile the code in the Bash on Ubuntu on Windows.
    
## RUN the code
- Make a build directory: mkdir build && cd build
- Compile: cmake .. && make
- Run it: ./mpc.
