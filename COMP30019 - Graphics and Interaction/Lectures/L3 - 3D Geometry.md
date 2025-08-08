

**Types of geometric data**:
- Explicit geometry:
	- Triangle meshes, patches, point clouds
- Implicit geometry
	- Parametric descriptions
	- Lines, curves, etc.
- Volumetric Data
	- Voxel grid (e.g. stack of images)
	- Medical image (e.g. MRI, CT)


# Polygon Meshes

## Basic Elements
- **Vertices**
	- 3D point that can include other meaningful data (e.g. colour, normal texture coords)
- **Edges**
	- Line segment connecting two vertices
- **Faces**
	- A planar element of a mesh bounded by edges (e.g. tri or quad)
- **Polygons**
	- Planar closed shape made of straight edges and vertices
- **Surfaces**
	- A continuous shape formed by a connected set of polygonal faces in a mesh

## Topology
- Which vertices are adjacent to a given vertex?
- Which triangles share a given vertex?
- Etc.
### Vertex-Vertex Meshes Representation
Represent an object as a set of vertices connected to neighbouring vertices
- Simple and lightweight
- Does not explicitly store faces and edges
- Efficient  for basic connectivity queries
- Not suitable for operations requiring edge or face topology

### Face-Vertex Meshes Representation
Represents an object as a set of faces, each defined by a list of vertex indices
- Widely used in mesh file formats, e.g. OBJ, PLY
- Efficient for storing geometry
- Suitable for many applications

### Polygon Data Format
- OBJ
- 3DS, FBX, DXF
- PLY, RAW
- MA/MB, BLEND
- WRL, WRZ

# The OBJ Format
- `#` -> Comments
- `v` -> Vertex (defined by `x y z (w)`, where `w` is optional - default = 1)
- `vt` -> Texture coordinate (`u (v w)` where `v` and `w` are optional - default = 1)
- `vn` -> Vertex normal - defined as `x y z`
- `f` -> Face - defined as `f v1 v2 v3`



# Normal Vectors

## Vertex Normals
The vertex normal is important for smooth shading using the Phong illumination model

Note that these aren't always provided by OBJ files

## Surface Normals

Winding order depends on the coordinate system
- Right-handed: counter-clockwise winding order for outward pointing normal
- Left-handed: clockwise winding is used to define front faces

We can compute vertex normals using the normalised sum of (unit) surface normals at the vertex

# Implicit and Parametric Geometry

Recall that any vector on a plane will be perpendicular to the plane's normal
- Hence we can define a plane as $\vec n \cdot \vec r = 0$
- Or more helpful: $\vec n \cdot (p_0 - \dot p) = 0$ where $p_0$ is a known point on the plane and $\dot p$ is any arbitrary point on the plane

One incredibly important application of parametric modelling is computing ray-plane intersections


## Volume Data
Typically stored on a 3D grid, where samples do not explicitly represent geometry, but rather sampled values across space








