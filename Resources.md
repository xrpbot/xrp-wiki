Resources
=========

Books
-----
* _R. Featherstone_: __Rigid Body Dynamics Algorithms__  
    Discusses algorithms for forward and inverse dynamics of rigid body systems, in particular joint space formulations. Introduces "spatial vectors".
* _J. Betts_: __Practical Methods for Optimal Control and Estimation Using Nonlinear Programming__  
    "Direct methods" for the generation of (locally) optimal trajectories. Reference for the basic algorithms behind PSOPT.

Software
--------
* [[Cartwheel 3D|https://code.google.com/p/cartwheel-3d/]]: Open source, physically realistic controller for humanoids, with a focus on computer animation rather than on real robots.
* [[trajopt|http://rll.berkeley.edu/trajopt/doc/sphinx_build/html/]]: Trajectory optimization for motion planning. Includes code to calculate quasi-static trajectories for walking on a simulated humanoid.
* [[Rigid Body Dynamics Library|http://rbdl.bitbucket.org/]]: Open-source implementation of many of the algorithms in Featherstone's book.
* [[Gazebo|http://www.gazebosim.org/]]: The Gazebo robot simulator, used in the DARPA challenge.

Robot competitions
------------------
* [[RoboCup|http://www.robocup.org/]]: An annual robot challenge with the eventual goal of producing robots capable of winning a soccer game against the most recent human world cup winner.
* [[DARPA robotics challenge|http://www.theroboticschallenge.org/]]: Humanoid robot challenge, organized by the US military, focused on disaster recovery.

Robot projects
--------------
* TUlip: Humanoid robot from TU Eindhoven, designed to participate in the RoboCup tournament. Relatively extensive documentation is available: see [[separate wiki page|/TUlip]].
* [[iCub|http://www.icub.org/]]: The iCub is a 1 metre high humanoid robot. Source code and CAD drawings are available. Unfortunately, it costs about 250,000€ to build. Also, it does not appear to be able to walk.

Papers
------
* [[E. Todorov|http://homes.cs.washington.edu/~todorov/]] works on optimization based control for humanoids and other robots. Many interesting papers, but unfortunately, no source code is available.
* [[T. Erez: Optimal Control for Autonomous Motor Behavior|http://openscholarship.wustl.edu/etd/101/]] (PhD thesis, 2011): Generate walking and running gaits for humanoids via numerical optimization.
* [[José-Luis Peralta et al.: Novel Design of Biped Robot Based on Linear Induction Motors|http://autsys.aalto.fi/en/attach/TheSway/Humanoids09_JLP.pdf]]: Using linear rather than ordinary (rotary) motors on a humanoid. Unfortunately, the high static power consumption does not make this approach look promising.