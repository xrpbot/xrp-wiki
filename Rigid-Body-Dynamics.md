Rigid Body Dynamics
===================

Introduction
------------

In order to develop robot controllers without having access to actual hardware, we perform simulations. These simulations take the output of the controller and calculate how it would cause the robot to move. The simulated movement is then fed back to the controller.

We model our robot as a collection of rigid bodies, connected together by joints. A rigid body, as the name implies, is a body that maintains its shape under all circumstances, i.e. it can only move as a whole, but it cannot bend or be compressed. Of course, there are no perfectly rigid bodies in reality - all physical objects deform when forces are applied to them. Predicting the deformation for a given force is the domain of so-called finite element methods (FEM). These methods require not only expensive computation, but also knowledge of the exact structure of the body (i.e. mass and stiffness distributions). In contrast, rigid body dynamics is much simpler and often a reasonable approximation. It is the method of choice for real-time physics engines such as [[ODE|http://www.ode.org/]] or [[Bullet|http://www.bulletphysics.org/]].

In this article, we will give a high-level overview of the principles of Rigid Body Dynamics. For details, the book by Featherstone is an excellent reference.

The free Rigid Body
-------------------

The objective of dynamics is to establish a relationship between the force applied and the resulting acceleration. You may remember the dynamics equation of a point mass from school, given by Newton's second law:
\begin{equation}
F = m a
\end{equation}
where \\(F\\) and \\(a\\) are three-dimensional vectors, because the point mass has three _degrees of freedom_ (DoFs) - that is, it can move in three different directions - and \\(m\\) is a scalar parameter, the mass.

In addition to three DoFs of translation, the rigid body has an additional three DoFs of rotation, for a total of six. This implies that accelerations and forces are now six-dimensional, with three angular and three linear components. In order to distinguish between (3d) linear velocities and (6d) combinations of angular/linear velocities, we refer to the latter as _spatial velocities_. Likewise, in addition to the (linear) force, a torque can act on it. Again, the combination of a torque and a linear force is called a _spatial force_.

Just like for forces acting on point masses, there is a superposition principle for spatial forces: any combination of forces and torques applied at arbitrary points of the rigid body can be written as a force and a torque applied to the center of mass.

The relationship between force and acceleration for the rigid body involves ten parameters. These are:</p>

* The total mass \\(m\\) (1 parameter)
* The position of the center of mass \\(c\\) (3 parameters)
* The moment of inertia tensor \\(I\\) (symmetric 3x3 matrix, i.e. 6 parameters).

Apart from these parameters, the shape of the rigid body is immaterial.

In contrast to the point mass, the equation of motion of the rigid body involves not only the spatial force \\((T, F)^\top\\) and the spatial acceleration \\((\alpha, a)^\top\\), but the spatial velocity \\((\omega, v)^\top\\) as well. It is called the [[Newton-Euler equation|http://en.wikipedia.org/wiki/Newton%E2%80%93Euler_equations]]. With respect to a coordinate frame whose origin is at the rigid bodies center of mass, it can be written as:
\begin{equation}
\left(\begin{array}{c}T\\\\F\end{array}\right) =
\left(\begin{array}{cc}I & 0\\\\0 & m \mathbf{1} \end{array}\right)
\left(\begin{array}{c}\alpha\\\\ a \end{array}\right) +
\left(\begin{array}{c}\omega \times I \omega  \\\\ \omega \times m v\end{array}\right)
\end{equation}

Joints and constraint forces
---------------------------

The effect of a joint is to constrain the relative motion of two rigid bodies. A ball-and-socket joint, for example, keeps points on two rigid bodies in the same position. The joint accomplishes this by exerting so-called constraint forces on the two bodies. The constraint forces are always such that the cause the constraint to remain satisfied.

In order to explain the concept of constraint forces, let us look at a very simple example: the pendulum. An idealized pendulum consists of a point mass and a massless rod (see figure). The massless rod connects the point mass to the pendulum support, forcing it to maintain a fixed distance \\(\rho\\) to it. Let us place our coordinate origin at the pendulum support and call the point mass position \\((x,y)\\). The constraint can the be written as
\begin{equation}
x^2 + y^2 = \rho^2
\end{equation}

Two forces are acting on the point mass: gravity and the constraint force due the constraint. The former, also called an active force, is easy to write down: F_g = FIXME.

The constraint force is harder to determine. We only know its effect on the motion: the constraint must remain satisfied. This alone cannot determine the constraint force, since the constraint is a scalar equation, but the constraint force is a two-dimensional vector. FIXME virtual work

Joint space dynamics
--------------------

Dealing with explicit constraint forces is cumbersome, so it would be desirable to have a way to eliminate them. This way is provided by joint space coordinates (also called generalized coordinates).

Let us go back to the pendulum example. If we specify the position of the point mass via \\(x\\) and \\(y\\), we can express configurations that are inconsistent with the constraint (e.g. \\(x = y = r\\))., and the constraint needs to be enforced explicitly. If, on the other hand, we introduce a new parameter \\(\phi\\) and let

\begin{eqnarray}
x &=& \rho \cos(\phi)\\\\
y &=& \rho \sin(\phi)
\end{eqnarray}

then the constraint is satisfied for any value of \\(\phi\\).

Kinematic tree dynamics
-----------------------

While we have used an extremely simple example, the general principle applies to much more complicated systems as well. We consider a kinematic tree, that is, a collection of rigid body connected by joints, in a tree-like form. The root of the tree is assumed to be fixed to the world frame.

It can be shown that the joint space dynamics take the form
\begin{equation}
\tau = M(q) \ddot{q} + C(q, \dot{q})
\end{equation}
where \\(M(q)\\) is called the mass matrix (due to the analogy with \\(F = ma\\)).

There are two possible problems we may wish to solve:

* __Forward dynamics:__ given \\(q\\), \\(\dot{q}\\) and \\(\tau\\), determine \\(\ddot{q}\\). By integrating \\(\ddot{q}\\) from known initial conditions to obtain \\(\dot{q}\\) and \\(q\\), this allows for simulation.
* __Inverse dynamics:__ given \\(q\\), \\(\dot{q}\\) and \\(\ddot{q}\\), determine \\(\tau\\). This allows to calculate the joint torques required to track a given trajectory.

The inverse dynamics problem is efficiently solved by the Recursive Newton-Euler algorithm. The algorithm works as follows:

* __Forward pass:__ Starting from the base of the kinematic tree, use the specified joint space velocities and accelerations to calculate the spatial velocities and accelerations of all the bodies in the tree.
* __Local pass:__ Using the Newton-Euler equations, calculate the total spatial forces acting on the bodies from the spatial velocities and accelerations.
* __Backward pass:__ The bodies at the leaves of the tree are attached to a single joint only. Since we know the total force acting on them, and the active forces, we can calculate the constraint force transmitted through the joint. Working upwards, the constraint forces transmitted through the child joints are known, and the constraint force transmitted through the parent joint can be calculated.
