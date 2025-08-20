
>[!Info] Note
> For this lecture, column major notation is used for vectors and matrices.
> 

Some useful applications for transformations are:
- Using different coordinate systems
- Hierarchical modelling
- Kinematics (forward and inverse)
- View control and projection

## Translation
- Additive
- Commutative
- Invertable

Graphics libraries like OpenGL have builtin functions for translation

## Rotation
- Additive
- Commutative *along the same axis*
	- Order matters for multiple rotations along different axes
- Invertable

Graphics libraries also have functions for this (pass in the angle amount and the axes)

# Homogeneous Coordinates
In Euclidean space, two parallel lines never intersect
In projective (perspective) space, paralell lines can meet at a point at infinity

>[!Info] Note
>Homogenous coordinates represent an N-dimensional point using N+1 numbers
>$$(x', y') \to (x, y, w)$$

A single euclidean point corresponds to infinitely many representations in homogeneous coordinates:
$$(1,2,3)=(2,4,6)=...=(a,2a,3a)$$
All represent the same Euclidean point $(1/3, 2/3)$ when converted back.

As a result, homogeneous coordinates are *scale invariant*
- Express projection in 3D graphics as a matrix equation
- Can represent points at infinity (when $w=0$)
	- E.g. $(x,y,z,0)^T$ can be interpreted as a point at infinity in the direction of $(x,y,z)^T$
	- $(x,y,z,0)^T$ can also be interpreted as a vector in the direction of $(x,y,z)^T$

$$[X,Y,Z,w]^T$$
## Euclidean vs. Affine Transformations
**Euclidean:**
- Preserves shape and size
- Translation, rotation, reflection

**Affine**:
- Preserves parallelism, colinearity, proportions
- Doesn't necessarily preserve lengths or angles
- Translation, rotation, reflection, scaling, shearing

### Inverse Transformations

We can convert transformation matrices to *Affine transformation matrix form*
$$
\begin{bmatrix}
\vec{p'} \\ 1
\end{bmatrix}
=
\begin{bmatrix}
\textbf{A} & \vec{b} \\ \vec{0} & 1
\end{bmatrix}
\begin{bmatrix}
\vec{p} \\ 1
\end{bmatrix}
$$
$$\vec{p'}=\textbf{A}\vec{p}+\vec{b}$$
An affine transformation is *invertible* iff **A** *is invertible*
- This requires $\det(\textbf{A}) \neq 0$
- Rotation, translation, scale, shearing are non-singular transformations

## Representing Rotations
In a 4x4 matrix, the upper-left 3x3 sub-matrix represents a *rotation*
- The first 3 elements of the fourth column represent the *translation*

One issue with the matrix representation of rotations is the inability to interpolate rotations

### Fixed Angle Representation
Rotation angles are applied about fixed global axes
- Order matters

### Euler Angles
Rotation angles are applied about moving (local) axes
- Order matters

#### Gimbal Lock
- Loss of one degree of freedom in 3D rotation
- Occurs when two rotation axes become parallel

### Quaternions
Avoid the issues of gimbal lock by generalising complex number transformations



