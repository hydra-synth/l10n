# Getting started

This page is an introduction to making live visuals using Hydra. It covers the basics of writing code in the browser to generate and mix live video sources. No coding or video experience is necessary! 

If you just want to start in 60 seconds you can also check:
* [Getting started short version](https://hackmd.io/@r08UjGF3QMCfvNmdjuY7iQ/rJCpsbNNc)

## Opening the editor
To get started, open the the [hydra web editor](https://hydra.ojack.xyz/) in a separate window.   Close the top window by clicking the [x] in the top right. 
![](https://i.imgur.com/ZfgVjJZ.gif)

You will see some colorful visuals in the background with text on top in the top left of the screen. The text is code that generates the visuals behind it. You can cycle through the visuals by clicking the shuffle button (add gif of cycling through sketches)

Modifying this code (as we will do in the next section) changes the visuals behind it. 


## First line of code

Use the ***clear all*** button to erase the previous sketch. Then, type or paste the following in the editor:

```javascript
osc().out()
```
Press  **‘ctrl + shift + enter’** to run this code. You should see some scrolling stripes appear on the screen. 

```hydra
osc().out()
```

This creates an oscillator[link to]

Inside the `osc()` parenthesis and in every source function you can modify parameters by putting a number inside the parentheses of `osc()`, for example, `osc(2)` 
![](https://i.imgur.com/ZfgVjJZ.gif)


```javascript
osc()
```



- Change parameters inside like ‘osc(2).out()’

```hydra
osc(2).out()
```
- Values can have decimal numbers
```hydra
osc(5,0.126,0.514).out()
```

## What is an error? 
Oh no! You have an error :( but don’t worry, if you have an error you’ll notice a label at the left-bottom on your screen. Something like ‘Unexpected token ‘.’ (in red) ’ will appear. This doesn’t affect your code, but you won’t be able to continue coding until you fix the error. Usually it is a typing error or something related to the syntax. 

## What is a comment?

### Single line comment:

```javascript
//Hello I’m a comment line. I’m a text that won’t change your code. You can write notations, your name or even a poem here.
```


## c) Adding transformations
```hydra
osc().rotate().out()
```

As you can see, you have first an input signal `osc()` and things that come after (`rotate()` and `out()`) are connected with a dot ‘.’
In this sense, Hydra is inspired by modular synthesis. Instead of connecting cables you connect different kinds of javascript functions.  
![](https://i.imgur.com/RBRxeiL.jpg)
###### source [Sandin Image Processor](https://en.wikipedia.org/wiki/Sandin_Image_Processor)



You can continue adding transformations like:  `osc().rotate().out()`. You can find more functions [here](/functions).
The logic is to initialize an input signal, then transformations (geometry and color transformations) and in the end always the output `.out(o0)` There are 4 output buffers that can be used: `.out(o0)` `.out(o1)` `.out(o2)` `.out(o3).`


## d) Using external sources
External sources can be used as a canvas inside Hydra, this can be: video, images, webcam, p5js, GLSL. In order to do this, first of all, external sources must be called with `s0.init` function. This doesn’t mean that you’ll see the effect instantly on your sketch. You need to call the source as you would do it with any input signal in the code. There are 4 input channels that can be used to introduce an external signal: s0, s1, s2, s3.

```javascript
s0.initCam() //webcam as external source
src(s0).out() //external source as canvas inside Hydra

s1.initImage('url image link') //image as an external source
src(s1).out(o0) //external image source as texture inside Hydra

s2.initVideo('url video link') //video as an external source
src(s2).out(o1) //external video source as texture inside Hydra

s3.initCam(1) //another webcam as an external source. Just change number in the parenthesis if you have more webcams connected
src(s3).out(o2)
```

## e) Multiple outputs 
Multiple outputs can be used, added or combined to each other. The available outputs are `.out(o0)` - `.out(o1)` - `.out(o2)` - `out(o3)`. To see all together use `render()`, to choose a specific output, for example `render(o1)`. Default buffer is `.out(o0)` = `.out() `

```hydra
gradient(1).out(o0)
osc().out(o1)
voronoi().out(o2)
noise().out(o3)
render()
```
![](https://i.imgur.com/m5Q0Na6.jpg)

*Trick: try to create different sketches and switch them in your live performance or even combine them.*

```hydra
gradient(1).out(o0)
osc().out(o1)
render(o0) //switch render output
// render(o1) 
```

## f) Blend modes between textures
In order to combine different output or textures you have several blend mode criteria.


```javascript
osc().blend(src(o1)).out() //mixes colors adds light but also opacity
noise().out(o1)
```
```javascript
src(o1).add(src(o3)).out(o2) //additive light. Color only gets brighterWhite intensity as priority  
noise().out(o1)
shape().out(o3)
```

```javascript
solid(0,0,1).diff(src(o1)).out(o0) //combines different signals by color difference (color negative/inverted/opposite).  
shape().out(o1)
```
```javascript
osc().mult(src(o1)).out() //subtract light. Black intensity as a priority.
shape(5).out(o1)

```
## g) modulate
`modulate()` An analogy in the real world, would be looking through a texture glass window.
`modulate()` does not change color or luminosity but shifts pixels by another texture; imagine looking through a bumpy glass window.

```hydra
osc().modulate(noise(3)).out()
```
### Try modulate with a camera!
```hydra
s0.initCam() //loads a camera

shape().modulate(src(s0)).out() //shape modulated by a camera
```
```hydra
s0.initCam() //loads a camera

src(s0).modulate(shape()).out() //camera modulated by a shape
```

### Save your sketch on the internet

Save your sketch as a URL on the internet with Hydra web editor. Use it to study, to perform or just to share with other people.
When you evaluate the entire code with `shift + ctrl + enter` Hydra generates automatically a URL that contains the last changes of your sketch. 
![](https://i.imgur.com/lV0rmoh.png)
Use `ctrl + l` to select the entire URL, then just `ctrl+c` to copy the link.


### Have fun!

---

# Glossary:
https://hackmd.io/RCr03ns1RXGa8GBn7BV8xQ



---


# 3. Additional topics (also short)

## live coding: evaluate separate lines or blocks of code

Press ‘ctrl+enter’ to run a line of code.  
Press ‘shift+ctrl+enter’ to evaluate the entire code.  
Press ‘alt+enter’ to evaluate a block of code.  
Tip: You can switch between different lines of code for a live coding performance.


```javascript
osc().out() //run this first

noise().mult(osc(10,0.1,10)).out() //now try this one
```

## Feedback
Output can be used as input source too. This process generates video feedback. Depending on which blend mode and the amount of values used, results can be very different and chaotic.
![](https://i.imgur.com/hdy3YJZ.jpg)
```javascript
osc().modulate(src(o0)).out()
```

```javascript
src(o0).scrollY(-0.001)
  .add(noise(30),0.001).out()
```

## a) arrays

Arrays in Hydra are a sequenced collection of values. You can use this to change several parameters in time just like a step sequencer.

```javascript
osc(10,0.1,[10,0,2,0.5]).out()

shape([3,4,200,2]).out()
```

## b) audio

Make audio reactive visuals using. The audio signal works as an input parameter, you can multiplicate this value in order to change the amount of changes.

```javascript
osc(20,0.1, ()=>a.ff[0]*10).out()
```


## d) screen capture
 `initScreen()` function is an external source that can be used in Hydra. Screen captures can be anything you choose to share, it can be a window tab from the browser, anything from your desktop, sticky notes, drawing softwares, video call meetings, or even Hydra in itself (which creates interesting feedback loops to play with). 

```javascript
s0.initScreen() //loads whatever you want to share as a source. Once is loaded is better to comment this line, in order not to run this everytime.

src(s0).kaleid(3).out() //load the source as a signal to play with in Hydra code
```


## e) atom-hydra
Hydra can be used without internet connection (or with it too) with Atom, this is a code editor. For using Hydra in this way, you need to install Atom and node.js in your computer, then search for the Hydra package inside Atom. This is also useful to run videos locally.

## f) custom javascript functions
Use custom javascript functions to control time parameters.
```javascript
osc(10,0.1,()=>Math.sin(time)*2).out()
shape().rotate(()=>time*0.5).out()
```


## h) p5.js
p5js library can be used in Hydra as an [external source]. Once p5js code is loaded into Hydra it can be used and combined with Hydra as a pattern or texture for example.

```javascript
p5 = new P5() // loads p5js library. Must be loaded just once, after running this line of code, it is better to comment it.

//loads p5’s draw function
p5.draw =()=>{
p5.ellipse(p5.windowWidth/2, p5.windowHeight/2,100)
}
p5.hide(); //hide p5 canvas, to use it just as texture in Hydra

s0.init({src:p5.canvas}) //load p5js as input source

src(s0).mult(osc()).out() //p5js source in Hydra as texture
```

## loadScript()
The await loadScript() function lets you load other packaged javascript libraries within the hydra editor. Any javascript code can run in the hydra editor.
## g) custom glsl functions 
Custom glsl functions can be used as custom functions
> [name=Flor de Fuego is okay to say function?]

functionshttps://hydra-book.glitch.me/#/glsl 

## f) hydra in a webpage
Hydra can be used inside a HTML site. Hydra’s functions could be modified by buttons, sliders, etc. [Here](https://hydra-webpage.glitch.me/) an example of how it can be used.



4. In-depth guides (How-to)

getting started (naoto)
- how to evaluate line
- sources (solid, gradient, osc, ...)
- evaluate different lines to live code
- color() to change color
- blending
- transform
- load images
- load webcam
additional topics
- modulate
- feedback
- arrays, functions
- sound (audio reactive)
- p5

