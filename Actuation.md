Actuation
=========

From the simulation, and from analysis of the TUlip robot, we can estimate the joint actuation requirements as follows:

* Power: around 200 W
* Angular velocity: around 5 rad/s
* Torque: around 100 Nm

The power requirement is not a large problem - with the advent of BLDC technology, lightweight motors with power in the kilowatt range are readily available. However, due to fundamental physics reasons, these motors produce power in the form of moderate torque at high angular velocities, making neccessary the use of gears.

For reference, let us look at the characteristics of a typical R/C BLDC motor ([[Propdrive 50-60 270KV|http://www.hobbyking.com/hobbyking/store/__22036__NTM_Prop_Drive_50_60_270KV_2400W.html]]):
* Max. current: 90A
* Max. voltage: 30V
* Max. power: 2400W
* Weight: 454g
* Kv: 270 rpm/V = 28.3 rad/(s*V), i.e. 849 rad/s @ max. voltage
* Km: 0.035 Nm/A (calculated), i.e. 3.15 Nm @ max. current

We can see that this motor would need a reduction by about one hundred to meet the above requirements. In professional robotics, one typically uses so-called strain wave gears to accomplish the task. These are, however, rather expensive. We have therefore settled, at least for now, on planetary gears.

A potential source for cheap planetary gears are cordless screwdrivers. Better ones are able to supply torques of several 10s of Nm.

In order to test various motor/gear combinations, we are setting up a motor test stand consisting of a load with a large moment of inertia to be accelerated and decelerated by a servo mechanism.