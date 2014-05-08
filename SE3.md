__Note:__ _this article is work in progress._

SE(3)
=====

Abstract
--------
In this article, we are going to discuss the Special Euclidean group SE(3) and its Lie algebra, se(3). These form the mathematical basis of rigid body transformations and velocities, respectively.

Rigid Body transformations
--------------------------
Let us consider all possible transformations between a _world frame_ and the _body frame_ of a given rigid body. As discussed elsewhere, every such transformation is the combination of a translation and a (proper) rotation, i.e.
\begin{equation}
x^\prime = Rx + c
\end{equation}
where \\(R\\) is a rotation matrix and \\(c\\) is a 3d vector.

Given such a transformation, we might wish to form its inverse (from the body frame back to the world frame), or we may wish to compose such transformations: given a transformation from the body frame of a rigid body A to the body frame of a rigid body B, and a transformation from B to C, we want to form the transformation from A to C.

The proper mathematical structure to capture this concept is a _group_. We therefore define SE(3), the Special Euclidean group, as the set of all transformations that can be applied to a rigid body, plus the operations of composing and inverting them:

SE(3), the special Euclidean group, is the group
\begin{equation}
\left\\{ (R,c), R \in \mathbb{R}^{3 \times 3}, c \in \mathbb{R}^3, R^\top R = 1, \det{R} = 1 \right\\}
\end{equation}

Group multiplication and inverse are given by:
\begin{eqnarray}
(R, c) \cdot (R^\prime, c^\prime) &=& (R R^\prime, R c^\prime + c)\\\\
(R, c)^{-1} &=& (R^\top, -R^\top c)
\end{eqnarray}

As mentioned above, SE(3) acts on vectors \\(x \in \mathbb{R}^3\\) via
\begin{equation}
\rho_{(R,c)}(x) = Rx + c
\end{equation}

The homogenous representation
-----------------------------
The action of SE(3) on vectors, as given above, is a bit awkward. We would prefer to express the action as a linear map (i.e. a matrix). The solution consists of considering augmented vectors, formed by 4-dimensional vectors with the fourth coordinate equal to 1, i.e.
\begin{equation}
\left(\begin{array}{c}x\\\\y\\\\z\\\\1\end{array}\right)
\end{equation}

On such vectors, SE(3) acts by the linear map
\begin{equation}
\rho_{(R,c)} = \left( \begin{array}{cc} R & c\\\\0 & 1 \end{array} \right)
\end{equation}

Such a mapping from (abstract) elements of SE(3) to linear maps is called a (linear) representation, 4-dimensional in this case. It is straightforward to verify that the abstract operations of group multiplication and inverse correspond to matrix multiplication and inverse, respectively. In particular, we have
\begin{equation}
\left( \begin{array}{cc} R & c\\\\0 & 1 \end{array} \right)^{-1} =
\left( \begin{array}{cc} R^\top & -R^\top c\\\\0 & 1 \end{array} \right)
\end{equation}
(Remember that \\(R^{-1} = R^\top\\).)

The Lie algebra se(3)
---------------------
In the next step, we would like to consider the velocity of a rigid body. The motion of a rigid body can be expressed as a curve in SE(3) which gives the transformation from the world to the body frame for each instant in time. Consider a curve that passes through the unit element at time \\(t = 0\\) (i.e. at \\(t = 0\\) the body frame is aligned with the world frame):
\begin{equation}
g: \mathbb{R} \to \mathrm{SE}(3),\;\;g(0) = 1
\end{equation}
The abstract derivative \\(g^\prime(0) := \left.\frac{\mathrm{d}}{\mathrm{d}t}\right|\_{t=0} g(t)\\) of all such curves at \\(t = 0\\) forms what is called the _tangent space_ of SE(3) at the unit element, which we call (lowercase) se(3).

Let us become more concrete by considering the homogeneous representation from above. In other words, curves now map $t \in \mathbb{R}$ to 4x4 matrices, no longer to abstract SE(3) elements. How would the derivative look like? To answer that question, we begin by considering the rotational part. Differentiating \\(R^\top R = 1\\) yields:
\begin{eqnarray}
&&\dot{R}^\top R + R^\top \dot{R} = 0\\\\
&&R^\top \dot{R} = -\dot{R}^\top R\\\\
&&R^\top \dot{R} = -(R^\top \dot{R})^\top
\end{eqnarray}
which implies that \\(\dot{R}^\top R\\) is skew-symmetric. If the curve is to pass through the unit element at \\(t = 0\\), then \\(R(0) = 1\\) and \\(R^\prime(0)\\) is therefore skew-symmetric. The derivative of the curve at \\(t = 0\\) thus has to look like:
\begin{equation}
\left(\begin{array}{cccc}
0 & -\omega_z & \omega_y & v_x\\\\
\omega_z & 0 & -\omega_x & v_y\\\\
-\omega_y & \omega_x & 0 & v_z\\\\
0 & 0 & 0 & 0
\end{array}\right)
\end{equation}
with a possibly confusing distribution of signs among the \\(\omega\\)s, the reason for which will become clear later. We call this the homogeneous representation of se(3).

It turns out se(3) is a vector space, i.e. its elements can be added and multiplied by scalars. Let us demonstrate this by using the homogeneous representation, the matrices of which can be added and multiplied by scalars in the usual way. Let \\(v \in se(3)\\) be represented by a curve \\(f(t)\\). \\(\alpha v\\) is then represented by the curve \\(f(\alpha t)\\), as implied by the chain rule. As to addition, let \\(v\\) and \\(w\\) be represented by curves \\(f(t)\\) and \\(h(t)\\). The curve \\(g(t) = f(t)h(t)\\) (which fulfills \\(g(0) = 1\\), as required) then represents \\(v + w\\), since, by the product rule,
\begin{equation}
g^\prime(0) = f^\prime(0) h(0) + f(0) h^\prime(0) = f^\prime(0) + g^\prime(0)
\end{equation}

A basis for se(3) is given by
\begin{eqnarray}
&&e_{\omega_x} = \left(\begin{array}{cccc}
0 & 0 & 0 & 0\\\\
0 & 0 & -1 & 0\\\\
0 & 1 & 0 & 0\\\\
0 & 0 & 0 & 0\end{array}\right),\;\;
e_{\omega_y} = \left(\begin{array}{cccc}
0 & 0 & 1 & 0\\\\
0 & 0 & 0 & 0\\\\
-1 & 0 & 0 & 0\\\\
0 & 0 & 0 & 0\end{array}\right),\;\;
e_{\omega_z} = \left(\begin{array}{cccc}
0 & -1 & 0 & 0\\\\
1 & 0 & 0 & 0\\\\
0 & 0 & 0 & 0\\\\
0 & 0 & 0 & 0\end{array}\right)\\\\
&&e_x = \left(\begin{array}{cccc}
0 & 0 & 0 & 1\\\\
0 & 0 & 0 & 0\\\\
0 & 0 & 0 & 0\\\\
0 & 0 & 0 & 0\end{array}\right),\;\;
e_y = \left(\begin{array}{cccc}
0 & 0 & 0 & 0\\\\
0 & 0 & 0 & 1\\\\
0 & 0 & 0 & 0\\\\
0 & 0 & 0 & 0\end{array}\right),\;\;
e_z = \left(\begin{array}{cccc}
0 & 0 & 0 & 0\\\\
0 & 0 & 0 & 0\\\\
0 & 0 & 0 & 1\\\\
0 & 0 & 0 & 0\end{array}\right)
\end{eqnarray}

For notational convenience, we introduce the hat operator that transforms from 6d column vectors to 4x4 matrices and (by a slight abuse of notation) vice versa. We adopt the angular-before-linear convention for the column vectors.
\begin{equation}
\widehat{\left(\begin{array}{c}
\omega_x\\\\
\omega_y\\\\
\omega_z\\\\
v_x\\\\
v_y\\\\
v_z
\end{array}\right)
} = \left(\begin{array}{cccc}
0 & -\omega_z & \omega_y & v_x\\\\
\omega_z & 0 & -\omega_x & v_y\\\\
-\omega_y & \omega_x & 0 & v_z\\\\
0 & 0 & 0 & 0
\end{array}\right)
\end{equation}

We refer to the elements of se(3) as spatial velocities.

The adjoint representation
--------------------------
The adjoint representation answers the question of how spatial vectors can be transformed from one frame to another. As before, ...

The exponential map
-------------------
\begin{equation}
\exp(\hat{\xi}) = \ldots
\end{equation}
