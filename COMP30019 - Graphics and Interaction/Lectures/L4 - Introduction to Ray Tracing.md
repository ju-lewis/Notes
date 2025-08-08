

# Rasterisation vs. Raytracing

## Rasterisation
- Common in interactive graphics (fast, GPU accelerated)
- Performs per-object and per-fragment shading separately
	- Vertex/fragment shaders
- Uses local illumination
- Rendering loop: iterate over objects

## Raytracing
- Used for photo-realistic rendering
	- Traditionally offline, but increasingly interactive with more hardware support
- Supports global illumination, accounting for full scene interactions (lights, materials, objects)
- Rendering loop: trace viewing rays (and secondary rays recursively)


# Stages of Ray-Tracing

1. **Ray Generation**
	- Cast a ray from the eye (camera) through each pixel on the screen to determine what it intersects
2. **Ray Traversal**
	- If the ray hits an object, spawn additional rays recursively
		- To check for shadows (shadow rays)
		- To compute reflections or refractions
3. **Shading**
	- If the intersection point is lit, compute its colour based on the light source(s)
4. **Blending**
	- Accumulate the colour from direct and recursive rays to determine the final pixel colour


## Recursive Ray-tracing
- Developed in 1980 by Turner Whitted
- Extends ray-casting by introducing recursion for handling:
	- Reflection
	- Refraction
	- Shadows



## Ray-Triangle Intersection

**Step 1: Ray-plane intersection**:
- Substitute ray equation into parametric plane equation (normal defined by cross product of edge vectors)
**Step 2: Check if P lies inside the triangle**:
- Barycentric Coordinates
	- Any point $P$ inside  a triangle with vertices A,B,C can be written as:
	- $P = uA + vB + wC$, where $u+v+w = 1$
	- If any $u,v,w < 0$, then the intersection is outside of the triangle



## Acceleration Structures
Efficient spatial structures reduce unnecessary intersection tests:
- Octree
- Kd-tree
- Bounding Volume Hierarchy

Trade-offs:
- Building structures takes time
- Dynamic scenes require careful handling
- Efficient update strategies needed for animated or changing regions


