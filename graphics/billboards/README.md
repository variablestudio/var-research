# Billboards

tldr: transform the model based on the the camera right and up vector (only right if you don't want bending e.g. trees)
the basic idea is described here:

http://gamedev.stackexchange.com/questions/113147/rotate-billboard-towards-camera
http://www.opengl-tutorial.org/intermediate-tutorials/billboards-particles/billboards/

Example implementation

```glsl
vec4 pos = vec4(aPosition, 1.0);
vec4 positionWorld = uModelMatrix * pos;
vec4 positionView = uViewMatrix * positionWorld;

vec3 right = vec3(uViewMatrix[0][0], uViewMatrix[1][0], uViewMatrix[2][0]);
vec3 up = vec3(0.0, 1.0, 0.0);
vec3 worldPos = aPosition.x * right + aPosition.y * up;

gl_Position = uProjectionMatrix * uViewMatrix * uModelMatrix * vec4(worldPos, 1.0);

```

