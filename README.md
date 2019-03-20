<a name="top"></a>
# CSS: Animation


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








































