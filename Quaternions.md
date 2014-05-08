Quaternions
-----------

Let \\(q = (a,b,c,d) = a + b\mathbf{i} + c\mathbf{j} + d\mathbf{k} \in \mathbb{H}\\).

* __Multiplication__: Quaternion multiplication is associative (\\(a(bc) = (ab)c\\)) and distributive (\\(a(b+c) = ab + ac\\)), but __not__ commutative (\\(ab \neq ba\\)).

* __Multiplication table:__ From \\(\mathbf{i}^2 = \mathbf{j}^2 = \mathbf{k}^2 = \mathbf{i}\mathbf{j}\mathbf{k} = -1\\), the whole multiplication table follows:

    <table>
    <tr><td>\(\mathbf{i}\mathbf{i} = -1\)</td>
    <td>\(\mathbf{j}\mathbf{i} = -\mathbf{k}\)</td>
    <td>\(\mathbf{k}\mathbf{i} = \mathbf{j}\)</td></tr>
    <tr><td>\(\mathbf{i}\mathbf{j} = \mathbf{k}\)</td>
    <td>\(\mathbf{j}\mathbf{j} = -1\)</td>
    <td>\(\mathbf{k}\mathbf{j} = -\mathbf{i}\)</td></tr>
    <tr><td>\(\mathbf{i}\mathbf{k} = -\mathbf{j}\)</td>
    <td>\(\mathbf{j}\mathbf{k} = \mathbf{i}\)</td>
    <td>\(\mathbf{k}\mathbf{k} = -1\)</td></tr>
    </table>

* __Conjugation:__ \\(q^\star = (a, -b, -c, -d)\\).

* __Norm:__ \\(||q|| = \sqrt{q q^\star} = \sqrt{q^\star q} = \sqrt{a^2 + b^2 + c^2 + d^2}\\). We have \\(||p q|| = ||p||\,||q||\\).

* __Inverse:__ \\(q^{-1} = \frac{q^\star}{||q||^2}\\). \\(q q^{-1} = q^{-1} q = 1\\).

* __Scalar and vector parts:__ \\(q = (r, v), r \in \mathbb{R}, v \in \mathbb{R}^3\\).
    \begin{eqnarray}
    (r_1, v_1) + (r_2, v_2) &=& (r_1 + r_2,\; v_1 + v_2)\\\\
    (r_1, v_1) \cdot (r_2, v_2) &=& (r_1 r_2 - v_1 \cdot v_2,\; r_1 v_2 + r_2 v_1 + v_1 \times v_2)
    \end{eqnarray}
    \\(q^\star = -q\\) iff \\(r = 0\\). Such quaternions are called _pure imaginary_.

* __Rotations:__ Let the vector \\((x, y, z)\\) correspond to \\(v = x\mathbf{i} + y\mathbf{j} + z\mathbf{k}\\). Rotations correspond to unit quaternions, \\(||q|| = 1\\), and act on vectors via \\(v^\prime = q v q^{-1}\\) (where \\(q^{-1} = q^\star\\) for unit quaternions). In matrix form, \\(q = (a,b,c,d)\\):
    \begin{equation}
    \left(\begin{array}{ccc}
    a^2+b^2-c^2-d^2 & 2bc-2ad         & 2bd+2ac        \\\\
    2bc+2ad         & a^2-b^2+c^2-d^2 & 2cd-2ab        \\\\
    2bd-2ac         & 2cd+2ab         & a^2-b^2-c^2+d^2\\\\
    \end{array}\right)
    \end{equation}

    Rotation by angle \\(\alpha\\) around (unit vector) \\(u\\) corresponds to \\(q = \cos(\alpha/2) + \sin(\alpha/2) u\\).

* __Angular velocity:__ By differentiating \\(q q^\star = 1\\), we obtain
    \begin{equation}
    \dot{q} q^\star = -(\dot{q} q^\star)^\star
    \end{equation}
    i.e. \\(\dot{q} q^\star\\) is pure imaginary. The vector component is:
    \begin{equation}
    \dot{q} q^\star = (0, \omega/2)
    \end{equation}
