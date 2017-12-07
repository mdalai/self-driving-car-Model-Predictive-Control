# self-driving-car-Model-Predictive-Control
- [CarND Term 2 Model Predictive Control (MPC) Project](https://github.com/udacity/CarND-MPC-Project)
- **Two objectives of MPC project**:
   - Speed: should come as close as possible to the desired speed based on the cost function.
   - How well the result is fitting 6 waypoints?

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

# MPC Algorithm
## Coordinates transformation
- Map Coordinates to Car coordinates
- [Great visualization](https://discussions.udacity.com/t/mpc-car-space-conversion-and-output-of-solve-intuition/249469/12).
