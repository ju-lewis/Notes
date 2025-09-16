
## Rendering Equation

>[!Warning] Problems with Whitted Illumination
>- Violates energy conservation
>- Hard shadows
>- Only considers direct illumination from light sources


**Rendering Equation**:

![[rendering-equation.png]]

### Bidirectional Reflectance Distribution Function (BRDF)
- Total energy of the reflected light will not exceed the energy of the incident light
	- Obeys law of energy conservation

![[brdf.png]]

BRDF can simply be applied to all light sources
- We need to measure the components of BRDF for different materials

The rendering equation is typically correct (photo-realistic)
- To solve it we discretise the function and calculate each light source separately
- Since there is randomness in the tracing, we take a given number of samples per pixel and average them out

