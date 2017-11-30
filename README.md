# self-driving-car-Model-Predictive-Control
- [CarND Term 2 Model Predictive Control (MPC) Project](https://github.com/udacity/CarND-MPC-Project)

# Install and run instructions
## Dependencies
- Follow [this instruction](https://github.com/udacity/CarND-MPC-Project).
- Follow [this instruction](https://github.com/udacity/CarND-MPC-Project/blob/master/install_Ipopt_CppAD.md) to install Ipopt and CppAD.
- Notes:
    - ```install_ipopt.sh``` would not work using /mnt/repo.. under Bash on Ubuntu WIN 10. You have to ```git clone``` the repo using Bash on Ubuntu WIN 10 AND execute ```install_ipopt.sh```.
    
## RUN the code
- Make a build directory: mkdir build && cd build
- Compile: cmake .. && make
- Run it: ./mpc.
