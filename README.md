Blog: https://blog.maximeheckel.com/posts/the-study-of-shaders-with-react-three-fiber/
Latest: https://thebookofshaders.com/05/


Fragment Shader

Shaders are the equivalent of the Guttenberg press
- Everything happens at once instead of defining things 1 by 1 by hand. (Printing press vs writing an entire page/book)

Shaders are fast because of parallel processing
- Each thread is blind and memoryless

GLSL = openGL Shading Language

Shader language has:
- Single main function that returns a color at the end
- gl_FragColor: final pixel color reserved global vairable
- has built in variables, functions and types (like gl_FragColor and vec4)
- vec4: RGBA values that are normalized between 0 and 1
- preprocessor macros. A pre-compilation step (#define global variables, #ifdef and #endif)
- float types: vital in shaders. More precision = better quality but longer to render (lowp, mediump, highp)
- automatic casting isnt a thing so ALWAYS type out decimals in your precision

Uniforms: data sent to every thread
- uniform vec2 u_resolution;  // Canvas size (width,height)
- uniform vec2 u_mouse;       // mouse position in screen pixels
- uniform float u_time;       // Time in seconds since load

glsl has hardware accelerated angle, trigonometric and exponential functions

gl_FragCoord: default input that holds the screen coordinates of the pixel or screen fragment that the active thread is currently working on
- you can normalize by dividing by the resolution


The real starting point (Section 5: Algorithmic Drawing)

attributes: inject different data for each attributes
- only available in the vertex shader

varyings: variable declared/set in the vertex shader to be read by the fragmentShader

pass attribute data to the fragment shader
1. Declare a varying in the vertex shader.
2. Assign the attribute to that varying variable.
3. Read the varying in the fragment shader.

UV coordinates is a coordinate system that allows you to position a 2D texture on a 3D object.