
Recall in the rasterization-based rendering pipeline:
- Scene data -> Vertex shader -> Geometry shader & assembly -> Rasterizer -> Fragment shader

Shading can happen in both the *vertex shader* and *fragment shader*

# Shading (Frequency) Model

## Per-Face Shading
- Shading once using face normal vector for all pixels on one triangle
- Leaves surface with faceted appearance

## Gouraud Shading
- Shading for each vertex on one triangle
- Interpolate the colours of three vertices for pixels inside the triangle

## Phong Shading
- Interpolate the normal vectors of each vertices for pixels
- Shading for each pixel


# Texture Mapping

The surface exists in the 3D world space
- Every 3D surface point also has a place where it goes in the 2D image and in the 2D texture

Each vertex is assigned a texture coordinate $(u,v) \in [0,1]$
- This is computed by the rasterizer

```
for each rasterized screen sample (x,y):
	(u,v) = evaluate texture coordinates at (x,y)
	float3 texcolor = texture.sample(u,v)
	set sample's color to texcolor
```

## Texture Mapping Sampling Methods

The most simple case is when the model is not scaled from its original size and the samples can be done 1:1 from screen space to texture space

If the model (and rasterized image) is scaled up (*magnified*) from the original, there are more screen samples than texture samples (because the objects take up more of the screen space)
- We need a way to handle the changing sample maps
- Nearest texel -> Simple, not ideal since it appears blocky
- Bilinear interpolation -> Take 4 nearest sample locations and interpolate texture colour

If the model is scaled down (*minified*) from the original, there are less screen samples than texture samples
- Supersampling can be used, but it's very expensive

