

## Curvilinear Coordinates


## Differential Forms

### Path Differential Form
$dS = | \ \vec{c} \ '(t) \ | \ dt$

### Surface Area
$dS = |det(T_u \times T_v)| \ du \ dv$

### Vector Differential Form
$d\vec{S} = \hat{n} \cdot dS$

#### For a surface in $\rm {I\!R}^3$:
$$\hat{n} = \frac{T_u\times T_v}{||T_u\times T_v||}$$
(Keep direction of parametrisation in mind)

#### For a path in $\rm {I\!R}^n$:


## Path Integrals
Integrating a scalar function over a path
$$
\int_{c}{f} \ dS = \int_{a}^{b}{f \ |\vec{c} \ '(t)| \ dt}
$$

Integrating a vector field over a path
$$\int_{c}{\vec{F}} \cdot d \vec{S} = \int_{a}^{b} \vec{F} \cdot \vec{c} \ '(t) \ dt$$

## Double/Triple Integrals



## Surface Integrals


## Integral Theorems
### ${\rm I\!R}^2$
$$Let \ \ \vec{F}=(P(x,y), \ Q(x,y))$$
**Green's Theorem**
	Cartesian Form:
$$\int_{\partial D}{ P \ dx + Q \ dy} = \iint_{D}{\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}}dxdy$$
	Vector Form:
$$\int_{\partial D}\vec{F} \cdot d \vec{S} = \iint_{D}{(\nabla \times\vec{F})} \cdot d \vec{S}$$
**Divergence Theorem:**

$$\int_{\partial D}{\vec{F}} \cdot d\vec{S} = \iint_{D}{\nabla \cdot \vec{F}} \ dS$$

### ${\rm I\!R}^3$
**Stokes' Theorem**
$$\int_{\partial S}\vec{F} \cdot d \vec{S} = \iint_{S}{(\nabla \times\vec{F})} \cdot d \vec{S}$$

Stokes' theorem relates the path integral around the boundary of an *open* surface to the surface integral. Green's Theorem is a special case of Stokes' Theorem where the surface is contained entirely in $\rm {I\!R}^2$.


**Gauss' Divergence Theorem**
$$\iint_{\partial  \Omega}{\vec{F} \cdot d \vec{S}} = \iiint_{\Omega}{\nabla \cdot \vec{F}} \ dV$$

Gauss' Divergence Theorem relates the volume integral to the surface integral of a bounded, closed shape in $\rm {I\!R}^3$