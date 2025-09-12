
## Mipmaps
Prepare textures at multiple resolutions
- Select the most appropriate one
- Level 0 is highest resolution

We can determine the level by computing $n = \log_2 L$ where $L$ is the 
![[mipmap.png]]

$n$ isn't necessarily an integer, hence we need to interpolate it (to avoid non-smooth transitions)
- We interpolate between the bilinear results of mipmap level $n$ and $n+1$
- This is trilinear interpolation

![[anisotropic-filtering.png]]

