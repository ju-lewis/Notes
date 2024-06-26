# Topics that need revision:
- Limits in $\mathbb{R}^3$ (Path finding strategies and sandwich theorem strategies, both for odd and even parities)
- Rules for continuity and differentiability
- Integration change of variables in $\mathbb{R}^2$
- Include double angle formulae in note sheet!
- Curvilinear coordinates! (Remember scale factors!! Unit vectors are normalised, so we need to multiply by the magnitude of the derivative)
- Revise multi-integrals where the vector field isn't defined at some point within the domain
- Conservative vector fields (only endpoints matter: $\phi(B) - \phi(A)$  )
- Proving vector calculus identities
- Gauss' Divergence Theorem requires a **closed solid** (we may need to add a 'base plate')

# Multivariate Limits
Showing a limit *doesn't* exist:
- Find 2 approach paths that have different limits (or don't exist)
	- The key for choosing the paths typically lies in how the terms are being linearly combined (e.g. addition of a cubic and quadratic)
Showing a limit *does* exist:
- For a very simple limit, we might just be able to rearrange
- Otherwise use sandwich (squeeze) theorem


# Vector Fields

# Applications of Differentiation

## Computing Extrema in $\mathbb{R}^3$

$Let \ f(x,y) : \mathbb{R}^2 \rightarrow \mathbb{R}^3 \text{ be a } C^1 \text{ function over domain }D$

For an *open* domain (bounded):
1. Compute $\nabla f$
2. Find solutions for $\nabla f = \vec 0$ within $D$
3. Compute Hessian determinant: $H(x,y) = (f_{xx})(f_{yy}) - (f_{xy})^2$
4. Classify nature of the extrema based on the Hessian determinant
	1. $H(x_0, y_0) > 0 \implies (x_0, y_0, z_0) \text{ is a minimum}$
	2. $H(x_0, y_0) < 0 \implies (x_0, y_0, z_0) \text{ is a maximum}$
	3. $H(x_0, y_0) = 0 \implies \text{the test is inconclusive}$

For the *boundary of a closed domain*:
1. Determine the boundary function: $g(x,y) = \partial D$
2. State the Lagrange Multiplier relation: $\nabla f = \lambda \nabla g$
$$(\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}) = \lambda \ (\frac{\partial g}{\partial x}, \frac{\partial g}{\partial y})$$
$$$$


# Curvilinear Coordinates
### Polar
$x = r \ cos\theta$
$y = r \ sin\theta$
### Cylindrical
$x = \rho \ cos\theta$
$y = \rho \ sin\theta$
$z=z$
### Circular
$x = r \ sin \theta \ cos \phi$
$y = r \ sin \theta \ sin \phi$
$z = r \ cos \theta$

## Converting Vector Fields to Curvilinear Coordinates:
1. Express the resultant vector in the curvilinear coordinates
2. Express the resultant vector as a linear combination of the curvilinear basis vectors
3. Solve simultaneously
## Converting Paths/Vectors to Curvilinear Coordinates:
1. Express the resultant vector in the curvilinear coordinates
2. Compute velocity vector 
3. Multiply by scale factors
4. Integrate with respect to t


# Differential Forms

### Path Differential Form
$ds = | \ \vec{c} \ '(t) \ | \ dt$

$d\vec{s} = \vec{c} \ '(t)dt$

### Surface Area
$dS = |det(T_u \times T_v)| \ du \ dv$

$d \vec{S} = (T_u \times T_v) \ dS$


#### For a surface in $\rm {I\!R}^3$:
$$\hat{n} = \frac{T_u\times T_v}{||T_u\times T_v||}$$
(Keep direction of parametrisation in mind)

#### For a path in $\rm {I\!R}^n$:


# Path Integrals
Integrating a scalar function over a path
$$
\int_{c}{f} \ dS = \int_{a}^{b}{f \ |\vec{c} \ '(t)| \ dt}
$$

Integrating a vector field over a path
$$\int_{c}{\vec{F}} \cdot d \vec{S} = \int_{a}^{b} \vec{F} \cdot \vec{c} \ '(t) \ dt$$

# Double/Triple Integrals


## Applications:
Centre of Mass:
$$x_{cm}=\frac{\iiint_{D}x \ \mu(x,y,z)dV}{\iiint_{D}\mu(x,y,z)dV}$$
$$y_{cm}=\frac{\iiint_{D}y \ \mu(x,y,z)dV}{\iiint_{D}\mu(x,y,z)dV}$$
$$y_{cm}=\frac{\iiint_{D}z \ \mu(x,y,z)dV}{\iiint_{D}\mu(x,y,z)dV}$$
Moment of Inertia:
$$x_{im} = \frac{\iiint_{D}{(y^2+z^2) \ \mu(x,y,z)}dV}{\iiint_{D}{\mu(x,y,z)}dV}$$


# Surface Integrals

$$\text{Surface area} = \iint_{\Phi}{1}\ dS$$
# Integral Theorems
### ${\mathbb{R}}^2$
$$Let \ \ \vec{F}=(P(x,y), \ Q(x,y))$$
**Green's Theorem**
	Cartesian Form:
$$\int_{\partial D}{ P \ dx + Q \ dy} = \iint_{D}{\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}}dxdy$$
	Vector Form:
$$\int_{\partial D}\vec{F} \cdot d \vec{S} = \iint_{D}{(\nabla \times\vec{F})} \cdot d \vec{S}$$
**Divergence Theorem:**

$$\int_{\partial D}{\vec{F}} \cdot \hat{n} \  d{S} = \iint_{D}{\nabla \cdot \vec{F}} \ dS$$
### ${\mathbb{R}}^3$
**Stokes' Theorem**
$$\int_{\partial S}\vec{F} \cdot d \vec{S} = \iint_{S}{(\nabla \times\vec{F})} \cdot d \vec{S}$$

Stokes' theorem relates the path integral around the boundary of an *open* surface to the surface integral. Green's Theorem is a special case of Stokes' Theorem where the surface is contained entirely in $\mathbb{R}^2$.


**Gauss' Divergence Theorem**
$$\iint_{\partial  \Omega}{\vec{F} \cdot d \vec{S}} = \iiint_{\Omega}{\nabla \cdot \vec{F}} \ dV$$

Gauss' Divergence Theorem relates the volume integral to the surface integral of a bounded, closed shape in $\mathbb{R}^3$