# shaderpark_dtx
this is a small demo on how to use the shaderpark tool, and a general introduction to thinking of shaders in 3 dimensions


## Shader intro 
![alt text](<images/Screenshot 2025-06-02 at 11.49.40 AM.png>)
![alt text](<images/Screenshot 2025-06-02 at 11.50.36 AM.png>)

shaders are a way of interfacing with GPU hardware, the "program" is a set of instructions for every pixel to follow, each pixel gets the same instructions, with the only differentiating factor being location 

![alt text](<images/Screenshot 2025-06-02 at 12.28.35 PM.png>)
![alt text](<images/Screenshot 2025-06-02 at 12.29.31 PM.png>) 
![alt text](<images/Screenshot 2025-06-02 at 12.33.33 PM.png>)
### [Drawing in 2 Dimensions](https://iquilezles.org/articles/distfunctions2d/)

### [Drawing in 3 Dimensions](https://iquilezles.org/articles/distfunctions/)

## A few quirks to writing shaders
### Datatypes
Shaders are a STRONGLY typed language, meaning that all variables must have their type declared when they are created

In JS you can type something like
```
let foo = [0,1,3,4,5...]
```
in shaders you are limited to whatever
```
vec3 red = vec3(1.0,0.0,0.0);
red.x = 1.0;
red.y = 0.0;
red.z = 0.0;
```
**Most of what we need to do in this demo will be done with**
```
float : (0.1456)
vec2 : (mouse.x , mouse.y)
vec3 : (r , g , b)
vec4 : (a , b , c , d)
```
### low-level
shaders come with very few built-in functions. In order to use some of the convenience functions usually available in js, one has to create them as functions yourself. 
#### Random
```
float random (vec2 st) {
    return fract(sin(dot(st.xy,
                         vec2(12.9898,78.233)))*
        43758.5453123);
}
```
#### Remapping
```
float map(float value, float min1, float max1, float min2, float max2) {
  return min2 + (value - min1) * (max2 - min2) / (max1 - min1);
}
```

### debugging
* You cannot `print or console.log` on a value or vector. Shaders are run per-pixel, so there is no globally accessible truth. 
It must simply compile, and affect the output visually.
* linting and failure to run the code will still throw errors


## Introducing abstraction
### Shaderpark
Shaderpark is an educational tool that is intends to abstract- away some of the hardship of writing shaders, especially shaders that render 3D graphics