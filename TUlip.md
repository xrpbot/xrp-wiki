The TUlip robot
===============

TUlip is a bipedal robot realized by Eindhoven/Delft/Twente university. The hardware is reasonably well documented, so it may serve as a starting point for our own design.

The robot has 6 DoFs per leg: a 3 DoF hip, a 1 DoF knee and a 2 DoF ankle. Ankle roll is passive, the other 5 DoFs are actuated.

Simulator
---------
Data for simulating TUlip in the [[Gazebo|http://www.gazebosim.org]] simulator is available at http://wiki.ros.org/Robots/TUlip. This includes masses, moments of inertia, joint positions, etc.

Construction
------------
A reasonably detailed drawing of the leg appears in [1]. As mentioned above, the ankle roll DoF is passive; ankle pitch and knee pitch are actuated by [[Bowden cables|http://en.wikipedia.org/wiki/Bowden_cable]]. The lower leg therefore contains no motors (only encoders).

The active lower leg DoF employ "series elastic actuation", i.e. there is a spring in series with the Bowden cable. [1] provides phase/magnitude plots of the effect of this.

The construction of the hip joint is described in [2]. The three hip DoF appear to be connected directly to the gears (no series elastic element).

[[Hi-res photo of the robot|http://makerspacetwente.files.wordpress.com/2011/10/dscn4505.jpg]].

Motors
------
According to [1], TUlip uses (brushed) [[Maxon RE30|http://www.treffer.com.br/produtos/maxon/motores/pdf/81.pdf]] motors. (We assume they use the 36V version, but this does not make a large difference.) The datasheet lists the motor properties as follows:

* Nominal speed: 7810 rpm (= 818 rad/s)
* Nominal torque: 83.4 mNm
* Stall torque: 936 mNm

[1] gives the bandwidth of the torque controller as 5-10 Hz.

The following table lists the reduction ratios of the various joints (from [1]; probably realized by planetary gears) and the resulting nominal speeds, nominal torques and stall torques (assuming ideal gears).

|Joint      |Power [W]|Reduction    |Nom. speed [rad/s]|Nom. torque [Nm]|Stall torque [Nm]|
|-----------|---------|-------------|------------------|----------------|-----------------|
|Ankle roll |0        |n/a (passive)|n/a               |n/a             |n/a              |
|Ankle pitch|60       |129          |6.3               |10.8            |121              |
|Knee pitch |60       |155          |5.3               |12.9            |145              |
|Hip roll   |60       |111          |7.4               |9.3             |104              |
|Hip pitch  |60       |222          |3.7               |18.5            |208              |
|Hip yaw    |60       |86           |9.5               |7.2             |80               |

References
----------
* [1]: [[D. Hobbelen et al.: System overview of bipedal robots Flame and TUlip|http://www.dutchrobotics.net/files/u1/HobbelenDeBoerWisse_IROS200.pdf]]
* [2]: [[M. Lamers: Redesign of the TULip hip joint|http://humanoid.tue.nl/wp-content/uploads/2011/09/MaartenLamers_INT2011_Redesign_of_the_TUlip_hip_joint.pdf]]
* [[TUlip in ROS wiki (simulator, etc.)|http://www.ros.org/wiki/Robots/TUlip]]
* [[TUlip paper index|http://www.techunited.nl/wiki/index.php?title=Humanoid]]
* [[D. Hobbelen: Limit Cycle Walking (PhD thesis, 2008)|http://repository.tudelft.nl/assets/uuid:deed5846-3db8-474f-9e71-628ce506dd4d/Hobbelen_20080530.pdf]]: has some construction details in appendix A
* [[ P. Heijkoop et al.: Dutch Robotics 2008 Teen-Size Team Description|http://www.dutchrobotics.net/files/u1/nds__Team_Description_paper_for_Robocup_2008.pdf]] (general overview)
* https://sites.google.com/site/rammakerspace/projects/reviving-tulip
