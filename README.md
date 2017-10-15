# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---


### Overview

MPC is a controller used to minimize the error between a predicted trajectory and a reference one by minimizing a cost function. Unlike, PID controller which relies on kinematic models of the process, MPC relies on dynamic models of the process. The main task of MPC controller is solving an optimization problem in which the control inputs (wheel angel and acceleration) should be chosen in such a way to give a predicted trajectory close to the reference one.
- The MPC controller consists of four components:
* Vehicle Model, dynamic model, which consists of a 6 component state vector as follows:
** x: x-axis of car position
** y: y-axis of car position
** psi: orientation
** v: car velocity
** cte: cross track error (offset from the lane center)
** epsi: orientation error

* constrains of the input signals, i.e. constraints on heading angel and acceleration. In our case the acceleration has two values {-1,1} and the heading angel is [-25,25].

* Trajectory: The predicted one based on the input value and the current state of a car. To get it a prediction horizon (T) should be determined and divided into N steps with a time step dt. In our case, after several tries, I found that with 12 step and 0.1 step size, I can get good results.

* Cost function: It is the core of the optimization problem. In any optimization problem or estimation problem, we should find, first of all, a cost function. Then, we should try to minimize it. In our case a cost function which is the sum of cross track and heading errors is used.

## Rubric Points

- **The Model**: *Student describes their model in detail. This includes the state, actuators and update equations.*

The kinematic model is described at lines 138-143 in [MPC.cpp](MPC.cpp).

- **Timestep Length and Elapsed Duration (N & dt)**: *Student discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. Additionally the student details the previous values tried.*

The values chosen for N and dt are 12 and 0.1, respectively. I choose these values after reading some discussions and by try and error.

- **Polynomial Fitting and MPC Preprocessing**: *A polynomial is fitted to waypoints. If the student preprocesses waypoints, the vehicle state, and/or actuators prior to the MPC procedure it is described.*

The waypoints are transformed  to the vehicle's perspective at lines 108-113 in [main.cpp](main.cpp), then processed

- **Model Predictive Control with Latency**: *The student implements Model Predictive Control that handles a 100 millisecond latency. Student provides details on how they deal with latency.*

Simply, I used the previous actuators value at previous time step. Lines 116-118 in [MPC.cpp](MPC.cpp).


** Finally, my code is based, basically, on the solution of Mind the line quiz in MPC lesson.

___

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `install-mac.sh` or `install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.

* **Ipopt and CppAD:** Please refer to [this document](https://github.com/udacity/CarND-MPC-Project/blob/master/install_Ipopt_CppAD.md) for installation instructions.
* [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page). This is already part of the repo so you shouldn't have to worry about it.
* Simulator. You can download these from the [releases tab](https://github.com/udacity/self-driving-car-sim/releases).
* Not a dependency but read the [DATA.md](./DATA.md) for a description of the data sent back from the simulator.


## Basic Build Instructions

1. cd build
2. Compile: `cmake .. && make`
4. Run it: `./mpc`.


## Call for IDE Profiles Pull Requests

Help your fellow students!

We decided to create Makefiles with cmake to keep this project as platform
agnostic as possible. Similarly, we omitted IDE profiles in order to we ensure
that students don't feel pressured to use one IDE or another.

However! I'd love to help people get up and running with their IDEs of choice.
If you've created a profile for an IDE that you think other students would
appreciate, we'd love to have you add the requisite profile files and
instructions to ide_profiles/. For example if you wanted to add a VS Code
profile, you'd add:

* /ide_profiles/vscode/.vscode
* /ide_profiles/vscode/README.md

The README should explain what the profile does, how to take advantage of it,
and how to install it.

Frankly, I've never been involved in a project with multiple IDE profiles
before. I believe the best way to handle this would be to keep them out of the
repo root to avoid clutter. My expectation is that most profiles will include
instructions to copy files to a new location to get picked up by the IDE, but
that's just a guess.

One last note here: regardless of the IDE used, every submitted project must
still be compilable with cmake and make./

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).
