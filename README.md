# Orbiting Planet Demo in three.js
*this project was completed for Andy Harris' Advanced Game development class*
## You can view the three.js scene [here](https://legoguy32109.github.io/three.js-orbiting-planet/)

This scene consists of:
- A purple planet surrounded by a ring
- A satellite orbiting that planet with a light source
- Multiple stars twinking in the distance also orbiting the planet
- Camera Controls to look around the planet

## Planet and ring...s?
To construct the planet, a purple sphere is simply placed at the origin or center of the scene. The ring was constructed using a 'ring' object, and a orange material with a small emission of light and low opacity was applied. The planet actually has multiple rings as the rings only render from one side, so another ring was cloned from the original, then flipped upside down. The rings slowly rotate around the planet thanks to this script applied to each.
```
Ring / Ring Rotate
function update( event ) {
	this.rotation.z += 0.003;
}
```

## The Satellite
The satellite is a more complex object orbiting the whole planet, and facing the planet with a light source illuminating it's surface. To accomplish the orbiting behavior the satellite is a child of a cube at the center of the origin. This cube is smaller than the sphere and is hidden from the viewer. A script on the cube rotates it around, and the offset satellite rotates with it, facing the planet at the same time.
```
Orbit Point for Satellite / Orbit
function update( event ) {
	this.rotation.z += -0.008;
}
```
The satellite consists of a series of cubes, scaled and translated to produce the arms and connecting bar of the satellite. Simple Diffuse Materials are applied to give it a somewhat realistic look.

![image](https://user-images.githubusercontent.com/37216503/152592018-8219611c-e9b7-46ed-830c-a843ee29cda9.png)

The satellite also has two children, one is the yellow point light shining on the planet's surface, and the other is a white point light who's range has been lowered, so it only illuminates the satellite. The satellite looked better in a white light but I wanted a more yellow light to illuminate the planet. The white light has been stretched abnormaly from being a child of a certain part of the satellite, but scaling a point light doesn't affect it.

## The Stars
The stars are octahedrons with a white, emissive material. The are all parented to another cube in the planet, that rotates very slowly. The stars themselves twingle by doing rotations about all their axis' at different speeds.
```
Star / Star Twinkle
function update( event ) {
	this.rotation.x += 0.01;
	this.rotation.y += -0.02;
	this.rotation.z += 0.002;
}
```
Here is the code for the slow rotation about the planet.
```
Orbit point for Stars / Star Orbit
function update( event ) {
 this.rotation.y += 0.0002;
}
```

## Camera Movement
To move the camera, I created a script for the scene and wrote two functions for aquiring the position of the mouse pointer, and another on initialization of the scene to place the camera at a certain set of xyz coordinates. The latter was done since wherever the editor camera view ended when selecting 'Play' would be where the camera was set during run time.
```
Scene / Camera Control
function init(){
	// set the position of the camera at a nice angle when the scene starts
	camera.position.x = 20;
	camera.position.z = 20;
	camera.position.y = 6;
}

function pointermove( event ) {
	// getting the camera to move is very difficult, this code was extended from the 'Camera' example in the three.js editor
	camera.position.x = ( event.clientX / player.width ) * 30 - 15;
	camera.position.y = ( event.clientY / player.height ) * 10 - 5;
	camera.lookAt(scene.position);
}
```

The camera position is controlled by the pointer of the mouse, whenever it is moved, that function runs which determines the location of the mouse in X and Y coordinates then respectively sets the camera's x and y position in the scene by a mathmatical formula checking the dimensions of the window the scene is running in and making sure the movements are the right magnitude to prevent viewer disorientation. **For best results try moving the mouse back and forth at the bottom of the screen**. The last step of that function is to make sure the camera is pointed at the origin, or `scene.position`, which is the focal point of the scene, the purple planet.

# Hope You Enjoy! 
