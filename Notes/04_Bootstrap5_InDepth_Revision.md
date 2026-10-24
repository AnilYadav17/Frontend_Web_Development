# Comprehensive Bootstrap 5 In-Depth Revision Guide 📦

> **Concept:** Bootstrap 5 is the world’s most popular front-end open-source toolkit. Version 5 is built with modern CSS custom properties, a robust 12-column flexbox grid system, pre-styled components, and **no jQuery dependency** (it uses pure Vanilla JavaScript and Popper.js).
>
> **Official Sources & References:**
> - Official Documentation: [getbootstrap.com/docs/5.3](https://getbootstrap.com/docs/5.3/)
> - Bootstrap Grid System Guide: [getbootstrap.com/docs/5.3/layout/grid](https://getbootstrap.com/docs/5.3/layout/grid/)
> - Bootstrap Components: [getbootstrap.com/docs/5.3/components](https://getbootstrap.com/docs/5.3/components/)
> - Bootstrap Icons: [icons.getbootstrap.com](https://icons.getbootstrap.com/)

---

## Table of Contents
1. [CDN Setup & Starter Template](#1-cdn-setup--starter-template)
2. [Breakpoints & Responsive Containers](#2-breakpoints--responsive-containers)
3. [The 12-Column Grid System In-Depth](#3-the-12-column-grid-system-in-depth)
4. [Utility Classes (Spacing, Sizing, Colors, Display)](#4-utility-classes)
5. [Flexbox Utilities in Bootstrap](#5-flexbox-utilities)
6. [Forms & Input Controls in Bootstrap 5](#6-forms--input-controls)
7. [Essential UI Components (Navbar, Cards, Modals, Accordions, Alerts)](#7-essential-ui-components)
8. [Bootstrap 5 Cheat Sheet & Exam Patterns](#8-bootstrap-5-cheat-sheet)

---

## 1. CDN Setup & Starter Template

In Bootstrap 5, you only need the CSS in the `<head>` and the bundle JS (which includes Popper.js) right before the closing `</body>` tag.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bootstrap 5 Revision</title>

    <!-- Bootstrap 5.3 CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Bootstrap Icons -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">
</head>
<body>

    <h1 class="text-center text-primary mt-4">Welcome to Bootstrap 5!</h1>

    <!-- Bootstrap 5.3 JS Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

---

## 2. Breakpoints & Responsive Containers

Bootstrap uses 6 default responsive breakpoints (mobile-first):

| Breakpoint | Infix | Dimensions | Target Devices |
|---|---|---|---|
| Extra small | *None* | `< 576px` | Portrait phones |
| Small | `sm` | `≥ 576px` | Landscape phones |
| Medium | `md` | `≥ 768px` | Tablets |
| Large | `lg` | `≥ 992px` | Desktops / Laptops |
| Extra large | `xl` | `≥ 1200px` | Large desktops |
| Extra extra large | `xxl` | `≥ 1400px` | Ultra-wide displays |

### Containers
Containers are required to pad content and house the grid:
- `.container`: Responsive fixed width (expands at each breakpoint).
- `.container-fluid`: Full width (`width: 100%`) at all viewport sizes.
- `.container-{breakpoint}`: Full width until the specified breakpoint, then fixed.

```html
<!-- Fixed centered container with automatic horizontal padding -->
<div class="container">
    <p>Content is boxed and centered.</p>
</div>

<!-- Edge-to-edge full width container -->
<div class="container-fluid">
    <p>Spans 100% of the screen width.</p>
</div>
```

---

## 3. The 12-Column Grid System In-Depth

The grid is built on a **12-column layout**. All columns (`.col-*`) must be immediate children of a `.row`.

```
+---+---+---+---+---+---+---+---+---+---+---+---+
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10| 11| 12|  (Total: 12 Units)
+---+---+---+---+---+---+---+---+---+---+---+---+
|      col-4 (33.3%)    |         col-8 (66.6%)         |
+-----------------------+-------------------------------+
|             col-6     |             col-6             |
+-------------------------------------------------------+
```

### Basic Responsive Grid Example
```html
<div class="container my-4">
    <div class="row">
        <!-- 100% on mobile, 50% on tablet, 33.3% on desktop -->
        <div class="col-12 col-md-6 col-lg-4 bg-light border p-3">Column A</div>
        <div class="col-12 col-md-6 col-lg-4 bg-light border p-3">Column B</div>
        <div class="col-12 col-md-12 col-lg-4 bg-light border p-3">Column C</div>
    </div>
</div>
```

### Equal-Width Columns & Auto-Width
```html
<div class="row">
    <!-- Equal split automatically (each takes 50%) -->
    <div class="col">Auto Split 1</div>
    <div class="col">Auto Split 2</div>
</div>

<div class="row">
    <!-- Variable width based on content -->
    <div class="col-auto">Takes only needed width</div>
    <div class="col">Takes all remaining space</div>
</div>
```

### Column Offsets & Row Columns
```html
<!-- Offsetting: Centers a 6-column box in a 12-column row -->
<div class="row">
    <div class="col-md-6 offset-md-3">
        Centered content (offset by 3 columns on medium screens)
    </div>
</div>

<!-- Row Columns: Quick grid of cards without specifying col on each card -->
<div class="row row-cols-1 row-cols-sm-2 row-cols-md-4 g-3">
    <div class="col"><div class="p-3 border">Card 1</div></div>
    <div class="col"><div class="p-3 border">Card 2</div></div>
    <div class="col"><div class="p-3 border">Card 3</div></div>
    <div class="col"><div class="p-3 border">Card 4</div></div>
</div>
```

### Gutters (Spacing between columns)
- `g-0` (no gap), `g-1` to `g-5` (default is `g-3` / 1.5rem)
- `gx-*` (horizontal column gap), `gy-*` (vertical row gap)

---

## 4. Utility Classes

### 1. Spacing Formula: `{property}{sides}-{size}`
- **Property**: `m` (margin), `p` (padding)
- **Sides**:
  - `t` (top), `b` (bottom), `s` (start/left in LTR), `e` (end/right in LTR)
  - `x` (left & right), `y` (top & bottom), *blank* (all 4 sides)
- **Size**:
  - `0`: 0
  - `1`: 0.25rem (4px)
  - `2`: 0.5rem (8px)
  - `3`: 1rem (16px)
  - `4`: 1.5rem (24px)
  - `5`: 3rem (48px)
  - `auto`: for centering block elements (`mx-auto`)

```html
<!-- Margin-top of 1.5rem, padding-x of 1rem, horizontally centered -->
<div class="mt-4 px-3 mx-auto" style="width: 300px;">Box</div>
```

### 2. Colors & Backgrounds
- Themes: `primary`, `secondary`, `success`, `danger`, `warning`, `info`, `light`, `dark`
- Text color: `text-primary`, `text-muted`, `text-white`
- Background color: `bg-primary`, `bg-light`, `bg-dark`
- Opacity utilities: `bg-opacity-75`, `bg-opacity-25`

### 3. Display & Sizing
- `d-none` (hidden), `d-block`, `d-inline`, `d-inline-block`, `d-flex`, `d-grid`
- Responsive display: `d-none d-md-block` (hidden on mobile, visible on tablet & up)
- Width & Height: `w-25`, `w-50`, `w-75`, `w-100`, `h-100`, `min-vh-100`

---

## 5. Flexbox Utilities

Quick flexbox formatting without writing custom CSS:

```html
<div class="d-flex justify-content-between align-items-center p-3 bg-light">
    <div>Left Logo</div>
    <div class="d-flex gap-3">
        <a href="#">Home</a>
        <a href="#">About</a>
        <a href="#">Contact</a>
    </div>
</div>
```

- **Direction**: `flex-row`, `flex-column`, `flex-row-reverse`
- **Justify Content**: `justify-content-start`, `justify-content-center`, `justify-content-end`, `justify-content-between`, `justify-content-around`
- **Align Items**: `align-items-start`, `align-items-center`, `align-items-end`, `align-items-stretch`
- **Gap**: `gap-1`, `gap-2`, `gap-3`, `gap-4`, `gap-5`

---

## 6. Forms & Input Controls

```html
<form class="p-4 border rounded shadow-sm bg-white">
    <!-- 1. Text input with floating label -->
    <div class="form-floating mb-3">
        <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com" required>
        <label for="floatingInput">Email address</label>
    </div>

    <!-- 2. Password input -->
    <div class="form-floating mb-3">
        <input type="password" class="form-control" id="floatingPassword" placeholder="Password" required>
        <label for="floatingPassword">Password</label>
    </div>

    <!-- 3. Select Dropdown -->
    <div class="mb-3">
        <label class="form-label" for="roleSelect">Select Role</label>
        <select class="form-select" id="roleSelect">
            <option selected>Choose...</option>
            <option value="1">Developer</option>
            <option value="2">Designer</option>
        </select>
    </div>

    <!-- 4. Checkbox / Switch -->
    <div class="form-check form-switch mb-3">
        <input class="form-check-input" type="checkbox" id="flexSwitchCheckDefault">
        <label class="form-check-label" for="flexSwitchCheckDefault">Subscribe to Newsletter</label>
    </div>

    <!-- 5. Submit Button -->
    <button type="submit" class="btn btn-primary w-100">Sign In</button>
</form>
```

---

## 7. Essential UI Components

### 1. Responsive Navbar with Mobile Collapse
```html
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container">
        <a class="navbar-brand fw-bold" href="#">MyBrand</a>

        <!-- Hamburger Toggler Button (Mobile) -->
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#mainNavbar">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="mainNavbar">
            <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
                <li class="nav-item"><a class="nav-link active" href="#">Home</a></li>
                <li class="nav-item"><a class="nav-link" href="#">Features</a></li>
                <li class="nav-item"><a class="nav-link" href="#">Pricing</a></li>
            </ul>
        </div>
    </div>
</nav>
```

### 2. Cards
```html
<div class="card shadow-sm" style="width: 18rem;">
    <img src="https://via.placeholder.com/300x150" class="card-img-top" alt="Card Header">
    <div class="card-body">
        <h5 class="card-title">Full Stack Masterclass</h5>
        <p class="card-text">Comprehensive guide covering Python, HTML, CSS, JS, and Bootstrap.</p>
        <a href="#" class="btn btn-primary">Enroll Now</a>
    </div>
    <div class="card-footer text-muted small">Updated 2 days ago</div>
</div>
```

### 3. Modals (Interactive Popup Dialog)
```html
<!-- Trigger Button -->
<button type="button" class="btn btn-danger" data-bs-toggle="modal" data-bs-target="#deleteModal">
    Delete Account
</button>

<!-- Modal Structure -->
<div class="modal fade" id="deleteModal" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title">Confirm Deletion</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                Are you sure you want to delete this permanently? This action cannot be undone.
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                <button type="button" class="btn btn-danger">Confirm Delete</button>
            </div>
        </div>
    </div>
</div>
```

### 4. Accordion (Collapsible FAQs)
```html
<div class="accordion" id="faqAccordion">
    <div class="accordion-item">
        <h2 class="accordion-header">
            <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#faq1">
                Is Bootstrap 5 dependent on jQuery?
            </button>
        </h2>
        <div id="faq1" class="accordion-collapse collapse show" data-bs-parent="#faqAccordion">
            <div class="accordion-body">
                No, Bootstrap 5 has completely removed jQuery in favor of modern native JavaScript.
            </div>
        </div>
    </div>
</div>
```

---

## 8. Bootstrap 5 Cheat Sheet & Exam Patterns

1. **Remember `ms-auto` vs `me-auto`**:
   - In Bootstrap 4 it was `ml-auto` / `mr-auto`. In Bootstrap 5, it became `ms-*` (margin-start / left) and `me-*` (margin-end / right) to support RTL (Right-to-Left) languages.
2. **Buttons**:
   - Standard: `btn btn-primary`, `btn btn-outline-secondary`
   - Sizes: `btn-sm`, `btn-lg`
3. **Tables**:
   - `table table-striped table-hover table-bordered`
4. **Badges & Alerts**:
   - `<span class="badge bg-success">Success</span>`
   - `<div class="alert alert-warning alert-dismissible fade show" role="alert">Warning alert! <button type="button" class="btn-close" data-bs-dismiss="alert"></button></div>`
