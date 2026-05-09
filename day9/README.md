# CSS Transitions - Day 9

## What are CSS Transitions?

CSS Transitions allow you to smoothly change CSS property values over a specified duration. Instead of property changes happening instantly, transitions create animated effects by gradually transitioning from the initial value to the final value.

---

## Why Use Transitions?

- **Better User Experience**: Smoother, more polished interfaces
- **Visual Feedback**: Users see what's happening (hover effects, clicks)
- **Easy to Implement**: Simple CSS, no JavaScript required
- **Performance**: Hardware accelerated in modern browsers

---

## Transition Syntax

### Basic Syntax
```css
selector {
    transition: property duration timing-function delay;
}
```

### Long Form (Individual Properties)
```css
selector {
    transition-property: background-color;
    transition-duration: 0.5s;
    transition-timing-function: ease;
    transition-delay: 0s;
}
```

---

## Transition Properties Explained

### 1. **transition-property**
Specifies which CSS property or properties should transition.

```css
/* Single property */
transition-property: background-color;

/* Multiple properties */
transition-property: background-color, width, height;

/* All properties */
transition-property: all;

/* None - disable transition */
transition-property: none;
```

**Common transitionable properties:**
- Color properties: `background-color`, `color`, `border-color`
- Size properties: `width`, `height`, `padding`, `margin`
- Position properties: `top`, `left`, `right`, `bottom`
- Transform: `transform`
- Opacity: `opacity`
- Border: `border`, `border-width`

---

### 2. **transition-duration**
How long the transition takes to complete, in seconds (s) or milliseconds (ms).

```css
transition-duration: 0.5s;    /* 500 milliseconds */
transition-duration: 1s;      /* 1 second */
transition-duration: 2000ms;  /* 2 seconds */
```

**Best Practices:**
- Fast interactions (hover): 0.3s - 0.5s
- Medium animations: 0.5s - 1s
- Slow animations: 1s - 3s
- Don't make transitions too long or they feel unresponsive

---

### 3. **transition-timing-function**
Controls the acceleration curve - how fast/slow the animation progresses.

#### Built-in Timing Functions:

| Timing Function | Behavior | Best Use |
|---|---|---|
| `ease` | Slow start, fast middle, slow end (DEFAULT) | General animations |
| `linear` | Constant speed throughout | Loading bars, continuous motion |
| `ease-in` | Slow start, accelerates to end | Element exiting viewport |
| `ease-out` | Fast start, decelerates to end | Element entering viewport |
| `ease-in-out` | Slow on both ends, fast in middle | Important transitions |
| `cubic-bezier(n,n,n,n)` | Custom curve | Fine-tuned animations |
| `steps(n)` | Animation in discrete steps | Game animations, pixel art |

**Example:**
```css
transition-timing-function: cubic-bezier(0.42, 0, 0.58, 1);
/* Same as ease */

transition-timing-function: steps(4);
/* Animation in 4 distinct steps */
```

---

### 4. **transition-delay**
Waits before starting the transition, in seconds (s) or milliseconds (ms).

```css
transition-delay: 0s;      /* No delay (default) */
transition-delay: 0.5s;    /* Wait 500ms before starting */
transition-delay: 1s;      /* Wait 1 second before starting */
```

**Use Cases:**
- Staggered animations (list items appearing)
- Creating sequential effects
- UI choreography

```css
li:nth-child(1) { transition-delay: 0s; }
li:nth-child(2) { transition-delay: 0.2s; }
li:nth-child(3) { transition-delay: 0.4s; }
```

---

## Complete Examples

### Example 1: Simple Button Hover
```css
button {
    background-color: blue;
    color: white;
    transition: background-color 0.3s ease;
}

button:hover {
    background-color: darkblue;
}
```

### Example 2: Multiple Properties
```css
.card {
    width: 200px;
    height: 200px;
    background-color: white;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    transition: all 0.3s ease;
}

.card:hover {
    width: 250px;
    height: 250px;
    background-color: #f0f0f0;
    border-radius: 10px;
    box-shadow: 0 10px 20px rgba(0,0,0,0.3);
}
```

### Example 3: Staggered List Animation
```css
li {
    opacity: 0;
    animation: slideIn 0.5s ease forwards;
}

li:nth-child(1) { animation-delay: 0s; }
li:nth-child(2) { animation-delay: 0.1s; }
li:nth-child(3) { animation-delay: 0.2s; }

@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateX(-20px);
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}
```

---

## Shorthand Syntax

```css
/* Single transition */
transition: background-color 0.5s ease 0.2s;

/* Multiple properties */
transition: 
    background-color 0.5s ease,
    width 0.3s linear,
    height 0.3s linear;

/* All properties with same duration */
transition: all 0.3s ease;
```

---

## Important Notes

1. **Performance Consideration**
   - Not all properties transition smoothly (use `transform` and `opacity` for best performance)
   - Avoid transitioning `width`, `height`, `left`, `right` if possible
   - Use `transform: scale()` instead of `width`/`height`

2. **Browser Compatibility**
   - Transitions are supported in all modern browsers
   - No prefix needed for modern browsers
   - Add prefixes for older browser support: `-webkit-`, `-moz-`, `-o-`

3. **Hardware Acceleration**
   - Use `transform` and `opacity` for better performance
   - These properties are GPU-accelerated

4. **Trigger Transitions**
   - `:hover` - mouse hover
   - `:focus` - element focus
   - `:active` - element click
   - JavaScript - change class or inline style
   - Media queries - responsive changes

---

## When to Use Transitions vs Animations

| Feature | Transitions | Animations |
|---|---|---|
| **Trigger** | Triggered by state change | Runs automatically or on demand |
| **Complexity** | Simple, 2-state changes | Complex, multi-step sequences |
| **Duration** | One time | Can repeat |
| **Use Case** | Hover effects, focus states | Loading spinners, sliders |

---

## CSS Transitions vs CSS Animations

### Transitions (simpler)
```css
.box {
    transition: all 0.3s ease;
}

.box:hover {
    transform: scale(1.2);
}
```

### Animations (more powerful)
```css
@keyframes grow {
    0% { transform: scale(1); }
    50% { transform: scale(1.1); }
    100% { transform: scale(1.2); }
}

.box {
    animation: grow 2s ease infinite;
}
```

---

## Best Practices

1. **Keep it Quick**: 0.3s - 0.5s for most interactions
2. **Use Appropriate Timing**: `ease` for general use, `ease-out` for entrance, `ease-in` for exit
3. **Subtle Movements**: Don't overdo animations
4. **Mobile Friendly**: Consider device performance, use shorter delays
5. **Accessibility**: Use `prefers-reduced-motion` media query
6. **Performance**: Stick to `transform` and `opacity` for smooth 60fps animations

```css
@media (prefers-reduced-motion: reduce) {
    * {
        transition: none !important;
        animation: none !important;
    }
}
```

---

## Summary

| Property | Values | Default |
|---|---|---|
| `transition-property` | property name, all, none | all |
| `transition-duration` | time (s, ms) | 0s |
| `transition-timing-function` | ease, linear, ease-in, ease-out, ease-in-out, cubic-bezier, steps | ease |
| `transition-delay` | time (s, ms) | 0s |

---

Created for practice on Day 9 - CSS Transitions Foundation
