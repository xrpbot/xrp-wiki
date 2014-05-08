Consider a rigid body in contact with the ground plane. Let the ground plane normal be \\(n\\). Let various contact forces \\(F_i\\) act on the rigid body at positions \\(r_i\\). The center of pressure is then defined as
\begin{equation}
x_c = \frac{\sum_i (F_i \cdot n) r_i}{\sum_i F_i \cdot n}
\end{equation}
where the generalization from finitely many forces to a force field should be obvious. As \\(F_i \cdot n \ge 0\\), the center of pressure must lie within the convex hull of the contact points \\(r_i\\).

Usually, we are given the total force and the total torque on the rigid body,
\begin{eqnarray}
F &=& \sum_i F_i\\\\
T &=& \sum_i r_i \times F_i
\end{eqnarray}
To calculate the center of pressure from these vectors, we note that
\begin{eqnarray}
n \times T &=& n \times \left( \sum_i r_i \times F_i \right) = \sum_i (n \times (r_i \times F_i))\\\\
&=& \sum_i \left( r_i (n \cdot F_i) - F_i (n \cdot r_i) \right)
\end{eqnarray}
As the contact points all lie in the plane, \\(n \cdot r_i\\) is equal for all \\(i\\). Let \\(n \cdot r_i =: h\\). Then
\begin{equation}
n \times T = \sum_i r_i (n \cdot F_i) - h \sum_i F_i = \sum_i r_i (n \cdot F_i) - h F
\end{equation}
Thus
\begin{equation}
x_c = \frac{n \times T + h F}{F \cdot n}
\end{equation}