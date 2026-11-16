# BARE-3d
BARE-3d (Basic Ascii Rendering Engine 3d) works using a raycasting technique to calculate the distance and angle from which an object (plane) is seen.  

## Render mechanics
### Referencials

The world and eye referencial are orthonormal basis of space defined by respectively $O,\vec{i},\vec{j},\vec{k}$ and $E,\vec{i'},\vec{j'},\vec{k'}$.
The eye referencial takes $\vec{i'}$ and $\vec{j'}$ as the coordinates axis for screen width and height, and $\vec{k'}$ as depth.

### Chaging referencial

To change a vector $\vec{v} = \begin{bmatrix} x & y & z \end{bmatrix}^T$ from basis $O,\vec{i},\vec{j},\vec{k}$ to basis $O',\vec{i'},\vec{j'},\vec{k'}$ with $\vec{i},\vec{j}$ and $\vec{k}$ already expressed with $\vec{i'},\vec{j'},\vec{k'}$ we can establish:

```math
\begin{gather*}
\vec{v} = x\vec{i} + y\vec{j} + z\vec{k} =
\begin{bmatrix}
\vec{i}_x & \vec{j}_x & \vec{k}_x \\
\vec{i}_y & \vec{j}_y & \vec{k}_y \\
\vec{i}_z & \vec{j}_z & \vec{k}_z
\end{bmatrix}
\begin{bmatrix}
x \\ y \\ z
\end{bmatrix} = 
\begin{bmatrix}
\vec{i}_xx + \vec{j}_xy + \vec{k}_xz \\
\vec{i}_yx + \vec{j}_yy + \vec{k}_yz \\
\vec{i}_zx + \vec{j}_zy + \vec{k}_zz
\end{bmatrix}
\end{gather*}
```

For the reverse operation, we need to solve the latest by inverting the vector base coordinate matrix.\
_(Check if in orthonormal base $M^{-1} = M^T$)_

For a point $H(x;y;z)$ we can convert it to a vector $\vec{v}$ and do the same operation with the addition of the vector representative of the origin point $\vec{O}$ expressed in the new base (with $\vec{i'},\vec{j'},\vec{k'}$):
```math
\begin{gather*}
\vec{H} = \vec{v} + \vec{O} = \begin{bmatrix}
\vec{i}_xx + \vec{j}_xy + \vec{k}_xz + \vec{O}_x \\
\vec{i}_yx + \vec{j}_yy + \vec{k}_yz + \vec{O}_y \\
\vec{i}_zx + \vec{j}_zy + \vec{k}_zz + \vec{O}_z
\end{bmatrix}
\end{gather*}
```

### Raycasting

A ray $R$ can be expressed as its parametric representation in the eye referencial with $\vec{v}$ it's direction vector and $E$ the origin of the eye. With $x_r$ and $y_r$ representing the coordinates on the  screen, and $d$ representing the screen distance from $E$:

```math 
\begin{gather*}
\vec{v} = \begin{bmatrix} 
x_r \\ y_r \\ d
\end{bmatrix}
\quad
R: \begin{cases} 
x = \vec{v}_x t + E_x \\
y = \vec{v}_y t + E_y \\ 
z = \vec{v}_z t + E_z 
\end{cases} 
= \begin{cases}
x = x_r t + E_x \\
y = y_r t + E_y \\ 
z = d t + E_z 
\end{cases}
\end{gather*}
```

In regard to that we can establish a value for $d$ in regard to the desired FOV. With $\theta$ being the FOV angle from the $z'$ axis and $s_w$ half the screen width: 

```math
\begin{gather*}
\tan(\theta) = \frac{s_w}{d} \iff d = \frac{s_w}{\tan(\theta)}
\end{gather*}
```

### Plane Intersection

The next step is to find the parameter $t$ on which the ray $R$ intersects a plane. We can express the plane $P$ on which we search for intersection as its parametric representation with $\vec{u}$ and $\vec{w}$ direction vectors of the plane and with $P_o(x_p;y_p;z_p)$ the plane's origin coordinates:

```math
\begin{gather*}
P: \begin{cases}
x = \vec{u}_x k + \vec{w}_x k' + x_p \\
y = \vec{u}_y k + \vec{w}_y k' + y_p \\
z = \vec{u}_z k + \vec{w}_z k' + z_p
\end{cases}
\end{gather*}
```

We can then represent $I$, the point of intersection as a linear equation where the parametric representation of $P$ and $R$ are equal:

```math
\begin{gather*}
I: \begin{cases}
x = \vec{u}_x m + \vec{w}_x m' + x_p = x_r t + E_x \\
y = \vec{u}_y m + \vec{w}_y m' + y_p = y_r t + E_y \\
z = \vec{u}_z m + \vec{w}_z m' + z_p = d t + E_z
\end{cases}
\iff
\begin{bmatrix}
\vec{u}_x & \vec{w}_x & -x_r \\
\vec{u}_y & \vec{w}_y & -y_r \\
\vec{u}_z & \vec{w}_z & -d
\end{bmatrix}
\begin{bmatrix}
m \\ m' \\ t
\end{bmatrix} 
= \begin{bmatrix} 
E_x - x_p \\ E_y - y_p \\ E_z - z_p
\end{bmatrix}
\end{gather*}
```

### Computation of $t$
Solving intersection by solving the whole system of equations is too costly to do each time so we can establish a formula to find only $t$ while computing as small thing as possible per ray and prefering to compute things on a per plane basis.

First, we can compute a normal vector to P using the cross product of its direction vectors
```math
\begin{gather*}
\vec{n} = \vec{u} \times \vec{w} = 
\lVert\vec{u}\rVert \lVert\vec{w}\rVert \sin(\widehat{\vec{u}\vec{w}}) \vec{n_u} = \lambda \vec{n_u} = 
\begin{bmatrix} 
\vec{u}_y \vec{w}_z - \vec{u}_z \vec{w}_y \\
\vec{u}_z \vec{w}_x - \vec{u}_x \vec{w}_z \\
\vec{u}_x \vec{w}_y - \vec{u}_y \vec{w}_x
\end{bmatrix}
\\[4pt]
\text{with} \; \vec{n_u} \; \text{a normal unit vector of} \; P 
\end{gather*}
```
Therefore we can say that $\vec{n} \cdot \vec{\delta} = 0$ then $\vec{\delta} \subset P$ which also implicates that:
```math
\begin{gather*}
\text{if} \;
\vec{n} \cdot \Bigl( 
\begin{bmatrix} X_x \\ X_y \\ X_z \end{bmatrix} -
\begin{bmatrix} x_p \\ y_p \\ z_p \end{bmatrix} 
\Bigr) = 0 
\iff
c = \vec{n} \cdot \vec{P_o} =
\vec{n} \cdot \vec{X} \; 
\text{then} \; X \in P
\end{gather*}
```

_(Note that here we use $\vec{X}$ to represent the vector associated to the point coordinates so that $\vec{X} = \begin{bmatrix} X_x & X_y & X_z \end{bmatrix}^T$)_\
So we want to solve for $t$ in our ray $R$:

```math
\begin{gather*}
\vec{n} \cdot \vec{R} =
\vec{n} \cdot \begin{bmatrix} x_r t + E_x \\ y_r t + E_y \\ d t + E_z \end{bmatrix} = c
\\[6pt]
\iff \vec{n}_x(x_r t + E_x) + \vec{n}_y(y_r t + E_y) + \vec{n}_z(d t + E_z) = c
\\[4pt]
\iff t(\vec{n}_x x_r + \vec{n}_y y_r + \vec{n}_z d) = 
c - (\vec{n}_x E_x + \vec{n}_y E_y + \vec{n}_z E_z)
\\[4pt]
\iff 
t = \frac{c - \vec{n} \cdot \vec{E}}{
\vec{n} \cdot \vec{v}} = 
\frac{\vec{n} \cdot \vec{P_o} - \vec{n} \cdot \vec{E}}{
\vec{n} \cdot \vec{v}} = 
\frac{\vec{n} \cdot (\vec{P_o} - \vec{E})}{
\vec{n} \cdot \vec{v}} \; \text{with} \; \vec{n} \cdot \vec{v} ≠ 0
\end{gather*}
```

_(Note that we can also find this equality using Cramer's rule)_\
We can therefore find the value of $t$ the parameter of $\vec{R}$ using per-plane constants $\vec{n}, P_o$ and $c$.

### Computation of $m$ and $m'$

We want to know the coordinates of the intersection point $\vec{I} = \vec{E} + t\vec{v} $ on $P$. Therefore we can express $\vec{q} = \vec{I} - \vec{P_o}$ wich ensures that $\vec{q} \subset P$. We can then express $\vec{q}$ since it is on the plane:
```math
\begin{gather*}
\vec{q} = m\vec{u} + m'\vec{w} 
\\
\iff \begin{cases}
\vec{u} \cdot \vec{q} = \vec{u} \cdot (m\vec{u} + m'\vec{w}) \\
\vec{w} \cdot \vec{q} = \vec{w} \cdot (m\vec{u} + m'\vec{w})
\end{cases}
\iff \begin{cases}
\vec{u} \cdot \vec{q} = m\vec{u}^2 + m'(\vec{u} \cdot \vec{w}) \\
\vec{w} \cdot \vec{q} = m(\vec{w} \cdot \vec{u}) + m'\vec{w}^2
\end{cases} 
\\[6pt]
\iff \begin{bmatrix} 
\vec{u}^2 & \vec{u} \cdot \vec{w} \\
\vec{w} \cdot \vec{u} & \vec{w}^2 
\end{bmatrix} 
\begin{bmatrix} m \\ m' \end{bmatrix} = 
\begin{bmatrix} 
\vec{u} \cdot \vec{q} \\
\vec{w} \cdot \vec{q}
\end{bmatrix}
\end{gather*}
```

We therefore need to solve the latest to find $m$ and $m'$ coordinates of $I$ on $P$. We can use cramer's for that:

```math
\begin{gather*}
A = \begin{bmatrix} 
\vec{u}^2 & \vec{u} \cdot \vec{w} \\
\vec{w} \cdot \vec{u} & \vec{w}^2 
\end{bmatrix}\!, \;
B = \begin{bmatrix} 
\vec{u} \cdot \vec{q} \\
\vec{w} \cdot \vec{q}
\end{bmatrix}\!,
\\[6pt]
\det(A) = \vec{w}^2 \vec{u}^2 - (\vec{u} \cdot \vec{w})^2 = \vec{w}^2 \vec{u}^2 - \vec{u}^2 \vec{w}^2 \cos(\widehat{\vec{u}\vec{w}})^2 = \vec{w}^2 \vec{u}^2 (1 - \sin(\widehat{\vec{u}\vec{w}})^2) = \vec{w}^2 \vec{u}^2 sin(\widehat{\vec{u}\vec{w}})^2 = \lVert\vec{n}\rVert^2
\\[6pt] 
m = \frac{\det(A_0)}{\det(A)} 
= \frac{(\vec{u} \cdot \vec{q})\vec{w}^2 - (\vec{w} \cdot \vec{q})(\vec{u} \cdot \vec{w})}{\det(A)} 
= \vec{q} \cdot \vec{u^*}, \; \vec{u^*} = \frac{\vec{u} \vec{w}^2 - \vec{w}(\vec{u} \cdot \vec{w})}{\det(A)}
\\[4pt]
m' = \frac{\det(A_1)}{\det(A)}
= \frac{\vec{u}^2 (\vec{w} \cdot \vec{q}) - (\vec{w} \cdot \vec{u})(\vec{u} \cdot \vec{q})}{\det(A)} 
= \vec{q} \cdot \vec{w^*}, \; \vec{w^*} = \frac{\vec{w} \vec{u}^2 - \vec{u}(\vec{w} \cdot \vec{u})}{\det(A)}
\end{gather*}
``` 
_(This assumes $\det(A) ≠ 0$ therefore that the plane's $\vec{u}$ and $\vec{w}$ direction vectors are not parallel and that none is equal to the null vector)_\
We can then compute $\det(A), \vec{u^*}$ and $\vec{w^*}$ on a per-plane basis, and find coordinates $I(m;m')$ on an per-intersection basis.

### Computation of hit angle cosine (light)

We can compute the cosine of the hit angle using the dot product between the direction vector $\vec{r}$ of the light ray $L$ emmited by the light and the normal vector $\vec{n}$ of $P$:

```math
\begin{gather*}
\vec{n} \cdot \vec{r} = \rVert \vec{n} \lVert \rVert \vec{r} \lVert \cos(\widehat{\vec{n}\vec{r}}) 
\iff \cos(\widehat{\vec{n}\vec{r}}) = \frac{\vec{n} \cdot \vec{r}}{\rVert \vec{n} \lVert \rVert \vec{r} \lVert}
\end{gather*}
```

We don't know on which side of $P$ $\vec{n}$ sits so we store both the cosine value (light level) and sign of the cosine (side of the plane) to determine when hitting the plane which side is lit.
The sign can be later compared to the sign of $\vec{n} \cdot \vec{v}$ to determine if we're seeing the same side as the lit side. 
