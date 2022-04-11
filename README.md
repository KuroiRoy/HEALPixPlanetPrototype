# HEALPixPlanetPrototype
Proof of concept for projecting square tiles onto a planet using shaders. Based on the article by Red Blob Games https://www.redblobgames.com/x/1932-sphere-healpix/

![Sphere with colored tiles](https://github.com/KuroiRoy/HEALPixPlanetPrototype/blob/015f1254ec7e30cd3429e720cab4aa810ff1b85d/ReadmeImage.png?raw=true)

## How it works
The project uses a shader graph for the PlanetTerrainShader with a subgraph for the HEALPix projection. The subgraph applies a specified mapping per tile in a longitude, cosine(latitude) space to a 3D vector on a sphere

![Projection from longitude/latitude to sphere](https://github.com/KuroiRoy/HEALPixPlanetPrototype/blob/0e4a853fff023c2baeab0280200a5455ef33840e/HEALPixFigure.png?raw=true)
