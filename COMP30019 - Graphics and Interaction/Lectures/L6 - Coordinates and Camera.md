
A frame of reference is defined by an origin and a set of basis vectors
- Basis is typically a set of orthonormal vectors


A point $p(x,y)$ can be represented with respect to a reference frame
- $p=O+x\textbf{X} + y\textbf{Y}$

## Transformations of Coordinate Frames

The rotation from frame (X,Y) to frame (X', Y') can be represented by a rotation matrix whose columns are basis vectors X' and Y'
- This is a very useful property for computing these change of basis operations


>[!Example] Recall
>A matrix $\textbf{M}$ is orthogonal if $\textbf{MM}^T=\textbf{M}^T\textbf{M}=\textbf{I}$


# Camera and View Transformations

Object space -> World space (modeling transformation)
World space -> Camera space (camera transformation)
Camera space -> Canonical view volume (Projection transformation)
Canonical view volume -> Screen space (Viewport transformation)

## Camera Transformation
- Convert world coordinates -> Camera coordinates
- Defines the view volume (frustum) for projection

## Projection Transformation
- Orthographic
- Perspective



