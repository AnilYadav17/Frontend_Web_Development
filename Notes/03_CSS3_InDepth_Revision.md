# Comprehensive CSS3 In-Depth Revision Guide 🎨

> **Concept:** CSS (Cascading Style Sheets) is the presentation language used to style, lay out, and animate HTML documents across diverse screens and devices.
>
> **Official Sources & References:**
> - MDN Web Docs - CSS: [developer.mozilla.org/en-US/docs/Web/CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)
> - CSS-Tricks Flexbox Guide: [css-tricks.com/snippets/css/a-guide-to-flexbox/](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
> - CSS-Tricks Grid Guide: [css-tricks.com/snippets/css/complete-guide-grid/](https://css-tricks.com/snippets/css/complete-guide-grid/)
> - W3C CSS Current Work & Specs: [w3.org/Style/CSS/current-work](https://www.w3.org/Style/CSS/current-work)

---

## Table of Contents
1. [CSS Syntax, Inclusion & The Cascade](#1-css-syntax-inclusion--the-cascade)
2. [Selectors, Combinators & Specificity Calculator](#2-selectors-combinators--specificity-calculator)
3. [The Box Model & Margin Collapsing](#3-the-box-model--margin-collapsing)
4. [CSS Units (Absolute vs Relative)](#4-css-units)
5. [CSS Positioning & Stacking Context (`z-index`)](#5-css-positioning--stacking-context)
6. [Flexbox Layout Complete Mastery](#6-flexbox-layout-complete-mastery)
7. [CSS Grid Layout Complete Mastery](#7-css-grid-layout-complete-mastery)
8. [Responsive Design & Media Queries](#8-responsive-design--media-queries)
9. [Transitions, Transforms & Keyframe Animations](#9-transitions-transforms--keyframe-animations)
10. [Modern CSS: Custom Properties (Variables) & Functions](#10-modern-css-custom-properties--functions)
11. [Cheat Sheet & Common Pitfalls](#11-cheat-sheet--common-pitfalls)

---

## 1. CSS Syntax, Inclusion & The Cascade

### Ways to Apply CSS
1. **External CSS** (Best practice):
   `<link rel="stylesheet" href="style.css">`
2. **Internal CSS**:
   `<style> p { color: blue; } </style>`
3. **Inline CSS**:
   `<p style="color: blue;">Hello</p>` (High specificity, difficult to maintain)

### The Cascade Priority (Lowest to Highest)
1. Browser user agent default styles
2. External / Internal stylesheets (evaluated in order of appearance)
3. Inline styles (`style=""`)
4. `!important` rule (overrides everything, use sparingly!)

---

## 2. Selectors, Combinators & Specificity Calculator

### Combinators
| Combinator | Syntax | Matches | Example |
|---|---|---|---|
| **Descendant** | `div p` | Any `<p>` inside `<div>` at any nesting depth | All nested paragraphs |
| **Direct Child** | `div > p` | Any `<p>` that is an immediate direct child of `<div>` | Only direct children |
| **Adjacent Sibling** | `h2 + p` | The first `<p>` placed **immediately** after `<h2>` | The very next paragraph |
| **General Sibling** | `h2 ~ p` | Any `<p>` that shares the same parent and follows `<h2>` | All subsequent siblings |

### Pseudo-Classes & Pseudo-Elements
- **Pseudo-classes** (State or position):
  - `:hover`, `:active`, `:focus`, `:focus-visible`
  - `:first-child`, `:last-child`, `:nth-child(2n)` (even), `:nth-child(odd)`
  - `:not(.active)`, `:checked`, `:disabled`
- **Pseudo-elements** (Virtual elements):
  - `::before`, `::after` (Must supply `content: ""` property)
  - `::placeholder`, `::selection`

### Specificity Hierarchy Formula `(Inline, ID, Class, Element)`
```
+-------------------------------------------------------+
|  Inline Styles      | ID Selectors | Classes/Attributes/Pseudo | Elements/Pseudo-elements |
|      (1, 0, 0, 0)   |  (0, 1, 0, 0)|        (0, 0, 1, 0)       |       (0, 0, 0, 1)       |
+-------------------------------------------------------+
```

**Examples:**
- `p` $\rightarrow$ `(0, 0, 0, 1)` = Specificity 1
- `.card` $\rightarrow$ `(0, 0, 1, 0)` = Specificity 10
- `div.card p` $\rightarrow$ `(0, 0, 1, 2)` = Specificity 12
- `#header .nav a:hover` $\rightarrow$ `(0, 1, 2, 1)` = Specificity 121
- `<h1 style="color: red;">` $\rightarrow$ `(1, 0, 0, 0)` = Specificity 1000

---

## 3. The Box Model & Margin Collapsing

```
+-------------------------------------------------------+
|                       MARGIN                          |
|   +-----------------------------------------------+   |
|   |                   BORDER                      |   |
|   |   +---------------------------------------+   |   |
|   |   |               PADDING                 |   |   |
|   |   |   +-------------------------------+   |   |   |
|   |   |   |            CONTENT            |   |   |   |
|   |   |   |          (width/height)       |   |   |   |
|   |   |   +-------------------------------+   |   |   |
|   |   +---------------------------------------+   |   |
|   +-----------------------------------------------+   |
+-------------------------------------------------------+
```

### `box-sizing: content-box` vs `border-box`
- **`content-box` (Default)**:
  $\text{Total Element Width} = \text{width} + \text{padding-left/right} + \text{border-left/right}$
  *(Causes elements to overflow containers when padding is added)*
- **`border-box` (Universal Modern Standard)**:
  $\text{Total Element Width} = \text{width}$ (Padding and border are absorbed inside the specified width)

```css
/* Universal Box-Sizing Reset - Always include in your CSS! */
*, *::before, *::after {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
```

### Margin Collapsing
When two vertical margins touch, they collapse into a single margin equal to the **largest** of the two margins (not their sum). Margin collapsing occurs only vertically on block elements, never horizontally.

---

## 4. CSS Units

| Unit | Type | Description |
|---|---|---|
| `px` | Absolute | Fixed device pixels (e.g., `16px`) |
| `%` | Relative | Relative to parent element's dimensions |
| `em` | Relative | Relative to the font size of the **immediate parent/current element** (compounds with nesting) |
| `rem` | Relative | **Root em**: Relative to `<html>` root font size (usually `16px`). **Best for typography & spacing!** |
| `vw` / `vh` | Viewport | 1% of the viewport width / height |
| `vmin` / `vmax` | Viewport | 1% of the minimum / maximum viewport dimension |
| `ch` | Relative | Width of the character "0" in the current font (great for reading measure, e.g. `max-width: 65ch`) |

---

## 5. CSS Positioning & Stacking Context

```css
/* 1. Static (Default) - Normal document flow */
.item-static { position: static; }

/* 2. Relative - Stays in flow, but offsets (top, left) relative to its original spot */
.item-rel { position: relative; top: 10px; left: 20px; }

/* 3. Absolute - Removed from flow, positioned relative to nearest positioned ancestor */
.parent { position: relative; }
.child { position: absolute; top: 0; right: 0; }

/* 4. Fixed - Positioned relative to viewport; does not scroll with page */
.navbar-fixed { position: fixed; top: 0; left: 0; width: 100%; z-index: 1000; }

/* 5. Sticky - Hybrid: acts relative until scroll threshold is reached, then sticks */
.table-header { position: sticky; top: 0; background-color: white; }
```

### `z-index` and Stacking Context:
- `z-index` only works on elements with a `position` other than `static` (or direct flex/grid items).
- Creates a new stacking context when opacity < 1, transform is set, or `isolation: isolate` is used.

---

## 6. Flexbox Layout Complete Mastery

Flexbox provides 1-dimensional layout control (along either row OR column).

```
Main Axis (default: horizontal ->)
+-------------------------------------------------------------------+
|  [Item 1]       [Item 2]       [Item 3]                           |
+-------------------------------------------------------------------+
Cross Axis (default: vertical | v)
```

### Flex Container Properties
```css
.flex-container {
    display: flex;
    flex-direction: row;          /* row | row-reverse | column | column-reverse */
    flex-wrap: wrap;              /* nowrap | wrap | wrap-reverse */
    justify-content: center;      /* Main Axis: flex-start | flex-end | center | space-between | space-around | space-evenly */
    align-items: center;          /* Cross Axis: stretch | flex-start | flex-end | center | baseline */
    align-content: stretch;       /* Multi-line cross axis alignment */
    gap: 1.5rem;                  /* Modern spacing between rows & columns */
}
```

### Flex Item Properties
```css
.flex-item {
    order: 2;                     /* Default 0. Determines display order */
    flex-grow: 1;                 /* Proportion of leftover free space to absorb */
    flex-shrink: 0;               /* Ability to shrink when space is scarce (0 = never shrink) */
    flex-basis: 250px;            /* Initial size before distribution */

    /* Shorthand: flex: grow shrink basis */
    flex: 1 1 250px;

    align-self: flex-end;         /* Overrides container's align-items for this specific item */
}

/* Perfect Centering in 2 lines: */
.center-box {
    display: flex;
    justify-content: center;
    align-items: center;
}
```

---

## 7. CSS Grid Layout Complete Mastery

CSS Grid is a 2-dimensional layout system (handles columns AND rows simultaneously).

```css
.grid-container {
    display: grid;
    /* Explicitly define columns: 3 equal flexible columns */
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: 100px auto 50px;
    gap: 20px;
}

/* Responsive Auto-Fit Grid without any Media Queries! */
.responsive-cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
}
```

### Named Grid Areas
```css
.dashboard-layout {
    display: grid;
    grid-template-columns: 240px 1fr;
    grid-template-rows: 60px 1fr 50px;
    grid-template-areas:
        "header  header"
        "sidebar main"
        "footer  footer";
    min-height: 100vh;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.footer  { grid-area: footer; }
```

### Spanning Grid Columns / Rows
```css
.hero-item {
    grid-column: 1 / -1;     /* Spans all columns from start to finish */
    grid-row: span 2;        /* Spans 2 rows down */
}
```

---

## 8. Responsive Design & Media Queries

### Mobile-First Approach (Recommended)
Write base styles for mobile screens first, then progressively enhance with `min-width` queries.

```css
/* Base styles (Mobile: 0px and up) */
.col { width: 100%; }

/* Tablets (≥ 768px) */
@media screen and (min-width: 768px) {
    .col { width: 50%; }
}

/* Desktops (≥ 1024px) */
@media screen and (min-width: 1024px) {
    .col { width: 25%; }
}

/* Dark Mode Preference */
@media (prefers-color-scheme: dark) {
    body {
        background-color: #121212;
        color: #f1f1f1;
    }
}
```

### Fluid Typography with `clamp()`
```css
/* clamp(MIN, PREFERRED, MAX) */
h1 {
    font-size: clamp(1.75rem, 4vw + 1rem, 3.5rem);
}
```

---

## 9. Transitions, Transforms & Keyframe Animations

### 1. Transitions (Smooth property interpolation on hover/change)
```css
.button {
    background-color: #3b82f6;
    color: white;
    /* transition: property duration timing-function delay */
    transition: background-color 0.3s ease, transform 0.2s ease;
}

.button:hover {
    background-color: #1d4ed8;
    transform: translateY(-3px) scale(1.02);
}
```

### 2. Transforms (Hardware-accelerated manipulation)
- `translate(x, y)`: Moves element without shifting document flow
- `scale(sx, sy)`: Scales size
- `rotate(45deg)`: Rotates element
- `skew(10deg)`: Distorts along axis

### 3. Keyframe Animations
```css
@keyframes pulseGlow {
    0% {
        transform: scale(1);
        box-shadow: 0 0 0 0 rgba(59, 130, 246, 0.7);
    }
    70% {
        transform: scale(1.05);
        box-shadow: 0 0 0 15px rgba(59, 130, 246, 0);
    }
    100% {
        transform: scale(1);
        box-shadow: 0 0 0 0 rgba(59, 130, 246, 0);
    }
}

.badge-live {
    animation: pulseGlow 2s infinite ease-in-out;
}
```

---

## 10. Modern CSS: Custom Properties & Functions

```css
:root {
    --primary-color: #4f46e5;
    --secondary-color: #ec4899;
    --font-base: 'Segoe UI', system-ui, sans-serif;
    --spacing-md: 1.5rem;
    --border-radius: 8px;
}

.card {
    font-family: var(--font-base);
    background-color: white;
    border-radius: var(--border-radius);
    padding: var(--spacing-md);
    border: 2px solid var(--primary-color);
    /* Dynamic calculations */
    width: calc(100% - var(--spacing-md) * 2);
}
```

---

## 11. Cheat Sheet & Common Pitfalls

1. **Flex vs Grid Quick Decision**:
   - Need alignment in **one dimension** (row or column)? $\rightarrow$ **Flexbox**
   - Need alignment in **two dimensions** (rows AND columns simultaneously)? $\rightarrow$ **CSS Grid**
2. **Horizontal Centering**:
   - Text / Inline elements: `text-align: center;`
   - Block element with fixed width: `margin: 0 auto;`
   - Flex container: `justify-content: center;`
3. **Height: 100% not working?**: Check if the parent container has an explicit height. Alternatively, use `min-height: 100vh`.
4. **`overflow: hidden`**: Used to clip overflowing content and clear floats.
