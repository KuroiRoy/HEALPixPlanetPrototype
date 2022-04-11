# HEALPixPlanetPrototype
Proof of concept for projecting square tiles onto a planet using shaders. Based on the article by Red Blob Games https://www.redblobgames.com/x/1932-sphere-healpix/

![Sphere with colored tiles](https://github.com/KuroiRoy/HEALPixPlanetPrototype/blob/015f1254ec7e30cd3429e720cab4aa810ff1b85d/ReadmeImage.png?raw=true)

## How it works
The project uses a shader graph for the PlanetTerrainShader with a subgraph for the HEALPix projection. The subgraph applies a specified mapping per tile in a longitude, cosine(latitude) space to a 3D vector on a sphere

![Projection from longitude/latitude to sphere](https://github.com/KuroiRoy/HEALPixPlanetPrototype/blob/0e4a853fff023c2baeab0280200a5455ef33840e/HEALPixFigure.png?raw=true)


It is not written in a very performant way. Ideally the mesh vertices would be converted into the longitude, cosine(latitude) space before being used. But for this small a prototype it's fine to do some extra trigonometry in the shader.

## Step by step
1. The builtin Plane object is a 10x10 square. We rotate it by 45 degrees and map the resulting vertices to [-1, 1]. This rotated range is usable in the HEALPix projection directly.
2. The material supplies the row and column for the HEALPix tiles, the shader supplies the correct mapping to a subgraph that matches the tile in that row and column.
3. As you can see in the image the top of the northern tiles is rectangular in the projection as opposed to the middle tiles where the top half is a triangle. The shader stretches the triangles into rectangles.
4. After mapping the x coordinate from [-1, 1] to the tile's range within [0, 2π] the x coordinate is used as the longitude on the sphere.
5. The y coordinate is mapped from [-1, 1] to the tile's range within [-1, 1] and then converted with arccosine
6. Then the longitude and latitude are used to create a 3D vector on the unit sphere.
7. And lastly the y value of the tile is used as the vertice's height on the sphere.