Acrobot
=======

Introduction
------------
The Acrobot is a relatively well-studied toy system for advanced control algorithms. It consists of a double pendulum where only the middle joint is actuated. The task for the controller is to drive the system from its rest position (i.e. hanging down) to pointing straight up.

There are a number of strategies that are specific to the Acrobot, for example [[energy-based swingup|http://www.clemson.edu/ces/crb/ece496/spring2002/group1a/acrobot_swingup.pdf]]. Since we are not interested in the Acrobot _per se_, we prefer to use black-box methods, i.e. generic methods that know nothing specifically about Acrobots.

Trajectory generation
---------------------
The first task is to generate a trajectory that will take the Acrobot from its rest position (hanging down) to the target position (pointing up) and can actually be executed, i.e. requires non-zero torque only at the middle joint.

In a nutshell, the method we use works as follows: we explicitly represent both the full state (two angles and two angular velocities) and the control input (torque applied to the middle joint) as a function of (discretized) time. The positions, velocities and torque at each point in time are taken as free variables in a high-dimensional optimization problem. We then add constraints that enforce dynamic consistency, i.e. that the change in position matches the velocity and the change in velocity matches the result of applying the torque.

We use the open-source [[PSOPT|http://www.psopt.org/]] software for trajectory generation, which in turn uses [[IPOPT|https://projects.coin-or.org/Ipopt]] as the optimizer.

Closing the loop
----------------
In an ideal world, applying the torque that results from the trajectory optimization to the Acrobot would result in it going from the start to the goal position. In the real world, that does not work, because small errors are not compensated and thus grow over time, resulting in the goal being missed. What we need is feedback - that is, we need to apply not the torque that would be appropriate if the ideal trajectory were tracked exactly, but the torque that is appropriate for the actual current state.

__Differential Dynamic Programming__ periodically re-executes the trajectory generation from the current state, seeding it with part of the last trajectory. Differential dynamic programming actually requires a rather complicated optimization problem in real time, requiring a fairly powerful computer.

The __LTV-LQR__ (Linear Time-Varing Linear Quadratic Regulator) technique generates a feedback law by linearizing the system dynamics around the nominal trajectory. The advantage of this method is that both the nominal trajectory and the feedback law can be computed off-line. Determining the actual feedback from the feedback law amounts to evaluting a dot product between the (time-varying) gains and the measured errors, which is very quick.