# CSS Transform - Day 10

## What is CSS Transform?

CSS Transform allows you to modify the appearance and position of elements in a 2D or 3D space. Transforms apply visual changes without affecting the document flow, making them excellent for creating interactive and dynamic layouts.

---

## Why Use Transform?

- **Performance**: Hardware accelerated, smooth animations
- **No Layout Reflow**: Elements stay in document flow
- **Complex Effects**: Rotate, scale, skew, translate in one property
- **Combines with Animations**: Perfect for smooth transitions
- **Mobile Friendly**: Works across all modern devices

---

## Transform Syntax

```css
selector {
    transform: function(value);
}
```

### Multiple Functions
```css
selector {
    transform: rotate(45deg) translate(20px, 30px) scale(1.5);
}
```

---

## 1. **rotate() - Rotation**

Rotates an element clockwise or counter-clockwise.

```css
/* Positive values = clockwise */
transform: rotate(45deg);      /* 45 degrees clockwise */
transform: rotate(180deg);     /* Flip upside down */
transform: rotate(-90deg);     /* 90 degrees counter-clockwise */
```

**Units:** degrees (deg), gradians (grad), radians (rad), turns (turn)

```css
transform: rotate(0.5turn);    /* Same as 180deg */
transform: rotate(3.14rad);    /* Approximately 180deg */
```

---

## 2. **translate() - Movement**

Moves an element from its current position without affecting other elements.

```css
/* Syntax: translate(x, y) */
transform: translate(50px, 100px);    /* Move 50px right, 100px down */
transform: translateX(50px);          /* Move only horizontally */
transform: translateY(100px);         /* Move only vertically */

/* Negative values move left/up */
transform: translate(-30px, -50px);
```

**Units:** pixels (px), percentages (%), em, rem, etc.

```css
transform: translate(50%, 100px);     /* 50% of element width, 100px down */
```

---

## 3. **scale() - Sizing**

Enlarges or shrinks an element.

```css
/* Syntax: scale(x, y) */
transform: scale(2);           /* Double size both directions */
transform: scale(1.5, 0.5);    /* 1.5x width, 0.5x height */
transform: scaleX(2);          /* Double width only */
transform: scaleY(0.5);        /* Half height only */

/* Less than 1 = shrink, Greater than 1 = enlarge */
transform: scale(0.5);         /* Half size */
transform: scale(1);           /* Normal size (no change) */
transform: scale(2);           /* Double size */
```

---

## 4. **skew() - Distortion**

Skews an element along X or Y axis.

```css
/* Syntax: skew(x-angle, y-angle) */
transform: skew(30deg);        /* Skew 30deg on X-axis */
transform: skew(30deg, 20deg); /* Skew on both axes */
transform: skewX(45deg);       /* Skew only X-axis */
transform: skewY(45deg);       /* Skew only Y-axis */
```

---

## 5. **Combining Transforms**

You can combine multiple transform functions:

```css
/* Multiple transforms applied in order */
transform: rotate(45deg) translate(20px, 30px) scale(1.5);

/* Order matters! */
transform: rotate(45deg) translate(50px);
/* Different from: */
transform: translate(50px) rotate(45deg);
```

---

## Transform-Origin

Controls the point from which transformation occurs (default is center).

```css
/* Syntax: transform-origin: x y; */
transform-origin: 0 0;         /* Top-left corner */
transform-origin: 50% 50%;     /* Center (default) */
transform-origin: 100% 100%;   /* Bottom-right corner */
transform-origin: top left;    /* Named values */
transform-origin: right;       /* Single value (vertical stays center) */
```

**Example:**
```css
div {
    transform-origin: top left;
    transform: rotate(45deg);
    /* Now rotates from top-left instead of center */
}
```

---

## 2D Transform Functions Summary

| Function | Purpose | Example |
|---|---|---|
| `rotate()` | Rotate element | `rotate(45deg)` |
| `translate()` | Move element | `translate(50px, 100px)` |
| `scale()` | Resize element | `scale(2)` |
| `skew()` | Distort element | `skew(30deg)` |
| `matrix()` | Combined transform | `matrix(1,0,0,1,50,100)` |

---

## Common Use Cases

### 1. Rotate on Hover
```css
img {
    transition: transform 0.3s ease;
}

img:hover {
    transform: rotate(360deg) scale(1.1);
}
```

### 2. Slide-in Animation
```css
div {
    transform: translateX(-100%);
    animation: slideIn 0.5s ease forwards;
}

@keyframes slideIn {
    to {
        transform: translateX(0);
    }
}
```

### 3. Flip Card Effect
```css
.card {
    transform: perspective(1000px) rotateY(0deg);
    transition: transform 0.6s;
}

.card:hover {
    transform: perspective(1000px) rotateY(180deg);
}
```

### 4. Scale on Click
```css
button {
    transform: scale(1);
    transition: transform 0.2s;
}

button:active {
    transform: scale(0.95);
}
```

---

## Transform vs Other Methods

| Method | Performance | Document Flow | Use Case |
|---|---|---|---|
| `transform` | ⭐⭐⭐ GPU accelerated | Unchanged | Animations, effects |
| `top/left` | ⭐ Slow reflow | Affected | Static positioning |
| `margin/padding` | ⭐⭐ Layout reflow | Affected | Spacing adjustments |
| `width/height` | ⭐⭐ Layout reflow | Affected | Resize elements |

**Best Practice:** Use `transform` for animations and interactive effects for best performance!

---

## Browser Support

- ✅ All modern browsers support 2D transforms
- ✅ CSS Transform property is stable and widely supported
- No vendor prefixes needed for modern browsers
- For older browser support, add prefixes:
  - `-webkit-` (Safari, Chrome)
  - `-moz-` (Firefox)
  - `-o-` (Opera)

```css
div {
    -webkit-transform: rotate(45deg);
    -moz-transform: rotate(45deg);
    -o-transform: rotate(45deg);
    transform: rotate(45deg);
}
```

---

## Performance Tips

1. **Use transform over position changes**: `transform: translate()` is faster than `top: 50px`
2. **Combine with transitions**: Smooth animations with minimal CPU usage
3. **Use will-change sparingly**: Hint browser to prepare for changes
   ```css
   div {
       will-change: transform;
       transition: transform 0.3s;
   }
   ```
4. **Avoid transforms on too many elements**: Can impact performance on low-end devices

---

## Summary Table

| Property | Values | Default |
|---|---|---|
| `transform` | function(value) | none |
| `transform-origin` | x-axis y-axis | 50% 50% |
| `transform-box` | border-box, fill-box, view-box | border-box |

---

Created for practice on Day 10 - CSS Transform Fundamentals
