# CSS: Animation
<a name="top"></a>

## 1. CSS Transforms

### CSS Transform Basics

- Transforms change the shape and position of the affected content

```scss
.blue_robot {
	
	// to the right 200px
	transform: translateX(200px);
	
	// to the right the width of the image
	transform: translateX(100%);
	
	// right 100px, down 300px
	transform: translate(100px, 300px);
	
	// 1- right 100px, down 300px
	// 2- distorts each image by a certain angle
	// 3- scale up 2x; (1x = 100% so no change)
	// 4- rotate 45deg clockwise
	transform: translate(100px, 300px) skew(20deg) scale(2) rotate(45deg);

	
	transform: scale(2) rotate(45deg) translate(100px, 100px) skew(20deg);
}
```

- The order matters! Transforms stack but it depends on the order that they appear
- [MDN: Skew](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/skew)

[[↑] Back to top](#top)

### Simple 3D Transforms

```css
.wrapper {
	margin: 2em auto 2em auto;
	perspective: 1000px;
}

img {
	display:block;
	margin: 0 auto;

	transform: rotateY(45deg) rotateX(35deg);
	/*transform: translate3d(100px, 200px, -1000px);*/
}
```

- Rotating the image and then adding perspective to the wrapper makes the image look 3D. **Cool effect I should remember.**
- [MDN Transform](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function)

[[↑] Back to top](#top)

### CSS Transitions

```scss
// original state
button {
	cursor: hand;
	background-color: #ff8d35;
	color: white;
	font:weight: 900;
	font-size: 1.2rem;
	border: none;
	padding:1em 3em;
	margin: 2em auto;
	display:block;
	
	// Transition code to hover state
	transition: background .5s ease-in, transform .5s .25s ease-in;
}

// hover state
button:hover {
	background: #c61140;
	transform: scale(1.2);
}
```

- Our transition property allows us to set specifically how we want the button to change. Our background will take 0.5 seconds and ease-in while our transform will wait 0.25 seconds before it starts its change, which also takes 0.5 seconds and will ease-in.

[[↑] Back to top](#top)

## 2. Understanding CSS Animations

### Animation Basics

- The two basic steps to a CSS Animation:
	+ define the animation
	+ Assign it to a specific element (or elements);
- Keyframes are a list describing what should happen over the course of the animation

```scss
.robot {
	animation-name: slide;
	animation-duration: 2s;
	animation-timing-function: ease-in;
	animation-iteration-count: 1;
}


@keyframes slide {
	from { transform: translateX(0); }
	to { transform: translateX(900px); }
}
```

[[↑] Back to top](#top)

### Use Animation-Delay and Animation-Fill-Mode

- `animation-fill-mode` tells the animation what to do outside of its animation
- [MDN: Animation-Fill-Mode](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-fill-mode)
	+ The `animation-fill-mode` CSS property sets how a CSS animation applies styles to its target before and after its execution.
- Here is a good summary of how it works:

![Animation fill mode](https://github.com/coolinmc6/css-animations/blob/master/assets/animation-fill-mode.png)

[[↑] Back to top](#top)

### Use Animation-Direction

- normal, reverse, alternate, alternate-reverse
- normal
	+ all iterations are played as specifically
	+ keyframes play from start to end
- reverse
	+ all iterations are played reverse direction
	+ keyframes play from end to start
- alternate
	+ the animation direction is alternated with each iteration of the animation
	+ keyframes play from start to end, then end to start, and continue alternating
- alternate-reverse
	+ the animation direction is alternated with each iteration of the animation
	+ just like alternate except end is first

```css
.robot {
	animation-name: slide;
	animation-duration: 2s;
	animation-timing-function: ease-in;
	animation-iteration-count: infinite;
	animation-fill-mode:forwards;
	animation-direction: alternate;
}

@keyframes slide {
	from {transform: translateX(0);}
	to {transform: translateX(900px);}
}
```

- the code above makes the robot move back and forth indefinitely

[[↑] Back to top](#top)

### Timing Functions and Easing

- animation-timing-function:
	+ predefined keywords
	+ cubic-bezier
	+ steps
- CSS Easing Keywords
	+ ease
	+ linear
	+ ease-in
	+ ease-out
	+ ease-in-out
- ease-in-out = `cubic-bezier(0.42, 0, 0.58, 1);`
- cubic-bezier(x1, y1, x2, y2);
- [cubic-bezier.com](http://cubic-bezier.com/#.17,.67,.83,.67)

[[↑] Back to top](#top)

## 3. CSS Animation Building Blocks

### Infinitely Looping Animation

```css
.fcloud01 {
	top:100px;
	z-index:100;
	/*animation-name: drift;
	animation-duration: 25s;
	animation-timing-function: linear;
	animation-iteration-count: infinite;*/

	animation: drift 25s linear infinite;
}
		
.fcloud02 {
	top:240px;
	z-index: 200;	

	animation: drift 35s 10s linear infinite backwards;
}



@keyframes drift {
	from { transform: translateX(-255px); }
	to { transform: translateX(1350px); }
}

```

- Notice how for cloud 2, the second number `10s` is the delay. For the `animation` property, the second number is always the delay. 
- After the name of the animation, the order doesn't matter, as long it matches a property appropriate for the animation....and the second number is always delay

[[↑] Back to top](#top)

### Animate an element into place

- This is a great effect and definitely one that I'd like to use somewhere: modal pop-in

```css
section {
  animation: slideIn .8s linear, fadeIn .4s ease-in;
}


@keyframes slideIn {
  0% { 
    transform: translateY(400px); 
    animation-timing-function: ease-out;
  }
  60% { 
    transform: translateY(-50px);
    animation-timing-function: ease-in; 
  }
  80% { 
    transform: translateY(10px); 
    animation-timing-function: ease-out;
  }
  100% { 
    transform: translateY(0); 
    animation-timing-function: ease-in;
  }
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
```

[[↑] Back to top](#top)

### Pause and Plan with Animation-Play-State

- This is very cool - using the `animation-play-state` to pause

```css
.sticker {
  width:200px;
  height:200px;
  position:absolute;
  background: url(sticker.png) top center no-repeat; 
  animation: spin 10s linear infinite;
  animation-play-state: paused;
}

.sticker:hover {
  animation-play-state: running;
}

@keyframes spin {
  /*0% {transform: rotation(0turn); }*/
  100% {transform: rotate(1turn); }
}
```

- In this scenario, I am giving the sticker an animation but it has `animation-play-state: paused;` so it's paused.
- On hover, I simply turn that to `running` and then it's like "adding an animation" on a hover state
- *Really cool little trick*


[[↑] Back to top](#top)


### Animate 3D Transforms

- The letter flip-up effect was also pretty cool. Here are the main items:

```css
div {
	perspective: 800px;
}
span {
	/* code */
	transform-origin: 50% 70%;
}

span:nth-child(1) {
  animation: flipUp 1s cubic-bezier(0.68, -0.55, 0.26, 1.55) both;
}

span:nth-child(2) {
  margin-right:30px;
  animation: flipUp 1s cubic-bezier(0.68, -0.55, 0.26, 1.55) .2s both;
}

span:nth-child(3) {
 margin-right:30px;
 animation: flipUp 1s cubic-bezier(0.68, -0.55, 0.26, 1.55) .4s both;
}

span:nth-child(4) {
  animation: flipUp 1s cubic-bezier(0.68, -0.55, 0.26, 1.55) .6s both;
}

span:nth-child(5) {
  margin-left:-28px;
  animation: flipUp 1s cubic-bezier(0.68, -0.55, 0.26, 1.55) .8s both;
 }

span:nth-child(6) {
  animation: flipUp 1s cubic-bezier(0.68, -0.55, 0.26, 1.55) 1s both;
}

span:nth-child(7) { 
  animation: flipUp 1s cubic-bezier(0.68, -0.55, 0.26, 1.55) 1.2s both;
}



@keyframes flipUp {
  from {transform: rotateX(90deg);}
  to {transform: rotateX(0deg);}
}
```

- First, notice the `perspective: 800px` on the parent div for the letters. Higher numbers like 800 - 1000px seem to be the best here
- Next, notice that the span has `transform-origin: 50% 70%;`
	+ first number is X, second is Y
	+ all fonts have some extra padding at the bottom, hence the 70% Y-mark is around the bottom of the letter
- The transform origin is the point all objects rotate around

[[↑] Back to top](#top)

### Prepare an image to use a sprite

- There are two lectures around this topic and I can't say I've ever really worked with sprites.
- I found this which might better help explain the animation concept of `steps()`:
	+ [How to Use steps() in CSS Animations](https://designmodo.com/steps-css-animations/)


[[↑] Back to top](#top)
 
### Chain Multiple Animations

- Chaining multiple animations is exactly how I thought it would work: you simply add a delay that is longer than your first animation. The final CSS for our letters animation is tedious so I'll only show the first few:

```css
span:nth-child(1) {
  animation:  flipUp 1s cubic-bezier(0.68, -0.55, 0.26, 1.55) both, 
              flipDown .5s cubic-bezier(0.45, 0.03, 0.51, 0.95) 2s forwards;  
}

span:nth-child(2) {
  margin-right:30px;
  animation: flipUp 1s cubic-bezier(0.68, -0.55, 0.26, 1.55) .2s both,
              flipDown .5s cubic-bezier(0.45, 0.03, 0.51, 0.95) 2.2s forwards;  
}

span:nth-child(3) {
 margin-right:30px;
 animation: flipUp 1s cubic-bezier(0.68, -0.55, 0.26, 1.55) .4s both,
               flipDown .5s cubic-bezier(0.45, 0.03, 0.51, 0.95) 2.4s forwards;  

/* 

code 

*/

}

@keyframes flipDown {
  /*from { transform: rotateX(0deg); }*/
  to { transform: rotateX(-180deg); }
}
```

- notice that for `flipDown`, because it is starting at its normal position, we don't even need to specify the `from` value.
- She recommends looking at SASS if you want to write things like this because you can create loops that will essentially write your CSS
- For animations with more than 3 or 4 steps, she recommends using JavaScript or JavaScript animation libraries

[[↑] Back to top](#top)



## 4. Applying CSS Animations to SVG 

### Prepare an SVG for animation

- Why SVG?
	+ resolution independent
	+ small file size
	+ accessibility
- Use Independent Shapes
	+ avoid merging paths
	+ layer shapes instead of knocking them out of the background shapes
- Keep drawings simple
	+ saves file size
	+ means easier animation
- Use Simple Shapes instead of Paths
	+ when possible, draw with shape tools
- Live text or outlined text?
	+ Live text is more accessible but may require web fonts to be loaded
	+ Outlined text may results in a smaller file size


[[↑] Back to top](#top)


### Animate SVG with CSS

- Most useful animatable properties
	+ SVG fill
	+ opacity
	+ CSS transforms on SVG elements
- Transform Origins
	+ HTML - at middle point (50%, 50%)
	+ SVG - top left of SVG canvas

[[↑] Back to top](#top)

## 5. Performance, Browser Support, and Fallbacks

### When to Use CSS Animations

- When to use CSS Keyframe Animation
	+ demonstrations or linear animations
	+ very simple state-based animation
- When to Use CSS Transitions
	+ toggling between two states
	+ animating on :hover, :active, :checked
- When to Use JavaScript
	+ complex state animations
	+ dynamic animations
		* change mid-way because of user input
	+ Physics -> anytime you're emulating physics, use JS
	+ Support older browsers
- What about SVG?
	+ vector-based animation
	+ icons or other self-contained animations
- Web Animation is a team effort
	+ don't have to choose just one web animation technology only
	+ combine JS for the logic and CSS for the motion
	+ Combine JS or CSS with SVG
- Consider Audience and Content
	+ how critical is the content?
	+ which browsers will your audience be using?
		* caniuse
- When Animations are Critical
	+ critical content + large percentage of less capable browsers
	+ Use JavaScript for older browser support
	+ [https://greensock.com/](https://greensock.com/)
- When Animation is not critical
	+ Progressive enhancement - animation for the users that have the capability

[[↑] Back to top](#top)

### High Performance Animations

- Most Performant Properties
	+ Opacity
	+ Scale, rotation and position with transform
- There are four steps a browser has to potentially go through to update any animations on the page
	+ Style
	+ Layout
	+ Paint
	+ Composite
- The fewer steps the browser has to go through, the more performant:
	+ See [CSS Triggers](https://csstriggers.com/) for a list of all of them
- The Translate 3D "Hack"
	+ turns on hardware acceleration
	+ promotes objects to a new layer
	+ `transform: translate3d(0,0,0)`
- The will-change property
	+ Notifies browsers that an object will be animating for priority rendering

[[↑] Back to top](#top)

### Code Organization and Fallbacks

- Handling Vendor Prefixes
	+ use an automated solution like autoprefixer
- Organizing CSS Animation Code
	+ Keep object specific animation code with the object's other styles
	+ If you use the same animations a lot, then centralizing the animation code that will be repurposed on multiple objects throughout a project is best
- Fallbacks and Olrder Browsers
	+ consider what your animated objects will look like if the animation is not performed
- Progressive Enhancement
	+ Think of animation as an enhancement for the browsers that support it
	+ Make sure less capable devices / browsers will get a functional website


[[↑] Back to top](#top)
 


## 6. Tools for Creating CSS Animations

### Helpful online tools for Animations

- [easings.net](https://easings.net/)
- [cubic-bezier.com](http://cubic-bezier.com/#.66,-0.57,.27,1.58)
- [The Sass Way](http://thesassway.com/)
- JavaScript Animation Library
	+ [GreenSock](https://greensock.com/)
	+ [Snap.svg](http://snapsvg.io/)
- SVG Editor
	+ [SVG OMG](https://jakearchibald.github.io/svgomg/)
- [Understanding SVG Coordinate Systems and Transformations (Part 1) — The viewport, viewBox, and preserveAspectRatio](https://www.sarasoueidan.com/blog/svg-coordinate-systems/)
- CSS Tricks
- [codrops](https://tympanus.net/codrops/)
- [CodePen](https://codepen.io/)


[[↑] Back to top](#top)



### Using Browsers' Animation Inspection Tools

[[↑] Back to top](#top)

