# CSS: Transforms and Transitions
<a name="top"></a>


## 1. Exploring Transitions

### Applying CSS Transitions

- `transition: property duration`

```scss
.item {
	transition: all 3s;
}
// same as:
.item {
	transition-property: all;
	transition-duration: 3s;
}
```

- for multiple transitions:

```scss
.item {
	transition: background-color 3s, width 2s, left 4s;
}
// same as:
.item {
	transition-property: background-color, width, left;
	transition-duration: 3s, 2s, 4s;
}
```


[[↑] Back to top](#top)


### Manage Transition Timing

- Transition Timings:
	+ ease
	+ linear
	+ ease-in
	+ ease-out
	+ ease-in-out
- cubic-bezier(x1, y1, x2, y2);


[[↑] Back to top](#top)

### Steps and Delays

- Step transitions
- `transition: property duration timing delay`
- Here are some examples:

```scss 

.item {
	transition: color 2s ease-in 0.5s;
	transition: width .5s linear 0s;
}

```

[[↑] Back to top](#top)

### Create an asymmetric transition

- to create an asymmetric transition, put the attractive transition on the hover and then "quick" one on the original to create that "pop-back" motion

[[↑] Back to top](#top)


## 2. Working with 2D Transformations



[[↑] Back to top](#top)

## 3. Working with 3D Transformations



[[↑] Back to top](#top)

## 4. Working in 3D Space


[[↑] Back to top](#top)













