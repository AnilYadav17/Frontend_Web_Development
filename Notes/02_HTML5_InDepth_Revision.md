# Comprehensive HTML5 In-Depth Revision Guide 🌐

> **Concept:** HTML (HyperText Markup Language) is the standard skeleton markup language that defines the structure and meaning of web content. HTML5 introduces semantic elements, native media playback, rich form validation, and modern web storage APIs.
>
> **Official Sources & References:**
> - MDN Web Docs - HTML: [developer.mozilla.org/en-US/docs/Web/HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)
> - WHATWG HTML Living Standard: [html.spec.whatwg.org/multipage/](https://html.spec.whatwg.org/multipage/)
> - W3C Web Accessibility Initiative (WAI-ARIA): [w3.org/WAI/standards-guidelines/aria/](https://www.w3.org/WAI/standards-guidelines/aria/)
> - Can I Use (Browser Support Matrix): [caniuse.com](https://caniuse.com/)

---

## Table of Contents
1. [HTML Document Anatomy & Boilerplate](#1-html-document-anatomy--boilerplate)
2. [Block-Level vs Inline vs Inline-Block Elements](#2-block-level-vs-inline-vs-inline-block-elements)
3. [HTML5 Semantic Elements (Layout & Accessibility)](#3-html5-semantic-elements)
4. [Forms, Input Controls & Validations In-Depth](#4-forms-input-controls--validations-in-depth)
5. [Regex (Regular Expressions) in HTML Form Pattern Attributes](#5-regex-pattern-validation)
6. [HTTP Methods in Forms (GET vs POST)](#6-http-methods-in-forms-get-vs-post)
7. [Tables & Data Presentation](#7-tables--data-presentation)
8. [Embedded Media (Audio, Video, Iframe, SVG)](#8-embedded-media)
9. [Web Storage, SEO & Accessibility (ARIA)](#9-web-storage-seo--accessibility)
10. [Cheat Sheet & Quick Reference](#10-cheat-sheet--quick-reference)

---

## 1. HTML Document Anatomy & Boilerplate

```html
<!DOCTYPE html>
<!-- Tells the browser this document is HTML5 (triggers standard rendering mode) -->
<html lang="en">
<head>
    <!-- Character encoding for all universal text & symbols -->
    <meta charset="UTF-8">

    <!-- Essential for Responsive Design: sets viewport width equal to screen width -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- SEO Meta Descriptions & Search Engine Directives -->
    <meta name="description" content="In-depth HTML5 revision guide with practical examples.">
    <meta name="keywords" content="HTML5, Semantic HTML, Web Development, Revision">
    <meta name="author" content="Student">

    <!-- Title shown on the browser tab -->
    <title>HTML5 In-Depth Master Revision</title>

    <!-- Base Tag: sets base URL & default target for all relative links -->
    <!-- <base href="https://example.com/" target="_blank"> -->

    <!-- External Stylesheet -->
    <link rel="stylesheet" href="style.css">
    <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
    <!-- Content displayed in the browser goes here -->
</body>
</html>
```

---

## 2. Block-Level vs Inline vs Inline-Block Elements

```
Block Element:
+--------------------------------------------------------+
| Takes full width available, always starts on a new line|
+--------------------------------------------------------+

Inline Elements:
[Takes only content width] [Sits next to each other] [No top/bottom margin or height]
```

| Characteristic | Block Elements | Inline Elements | Inline-Block |
|---|---|---|---|
| **Starts on new line?** | ✅ Yes | ❌ No (flows horizontally) | ❌ No (flows horizontally) |
| **Default Width** | 100% of parent container | Width of its content | Width of its content |
| **Can set width / height?** | ✅ Yes | ❌ No (ignored) | ✅ Yes |
| **Margin / Padding** | Top, Right, Bottom, Left | Left & Right only | Top, Right, Bottom, Left |
| **Common Examples** | `<div>`, `<p>`, `<h1>`-`<h6>`, `<header>`, `<footer>`, `<section>`, `<ul>`, `<li>` | `<span>`, `<a>`, `<strong>`, `<em>`, `<label>`, `<code>`, `<mark>` | `<img>`, `<button>`, `<input>`, `<select>`, `<textarea>` |

---

## 3. HTML5 Semantic Elements

Semantic tags convey **meaning to both developers and assistive technologies (screen readers, search engines)** rather than just being generic layout containers like `<div>`.

```
+-------------------------------------------------------------+
|                      <header>                               |
|        [Logo / Site Title]    <nav> Navigation Links        |
+-------------------------------------------------------------+
|                                  |                          |
|             <main>               |         <aside>          |
|  +----------------------------+  |  (Sidebar, Related links,|
|  |         <article>          |  |   Author info, Ads)      |
|  |  [Self-contained post]     |  |                          |
|  +----------------------------+  |                          |
|  |         <section>          |  |                          |
|  |  [Thematic grouping]       |  |                          |
|  +----------------------------+  |                          |
+-------------------------------------------------------------+
|                      <footer>                               |
|    (Copyright, Contact info, Policy links, <address>)       |
+-------------------------------------------------------------+
```

### Detailed Breakdown of HTML5 Semantic Tags

1. **`<header>`**: Header for a page or an `<article>`, usually containing a logo, headings, or search form.
2. **`<nav>`**: Reserved strictly for major site navigation links.
3. **`<main>`**: Represents the unique, core central content of the document. Only **one** `<main>` per page.
4. **`<article>`**: Represents complete, independent, self-contained content that can be distributed on its own (e.g., blog post, news article, forum comment, product card).
5. **`<section>`**: Groups related thematic content with a heading (e.g., Features section, Testimonials section).
6. **`<aside>`**: Secondary content tangentially related to the content around it (sidebars, callout quotes, advertising).
7. **`<footer>`**: Contains author info, copyright notice, contact links, sitemap links.
8. **`<address>`**: Specifically used to mark contact information for the author/owner of the document or article.
   ```html
   <address>
       Written by <a href="mailto:contact@tech.com">John Doe</a>.<br>
       Tech Tower, Bengaluru, India
   </address>
   ```
9. **`<figure>` and `<figcaption>`**: Encapsulates self-contained media (image, chart, code snippet) with an accessible caption.
   ```html
   <figure>
       <img src="chart.png" alt="Sales growth in Q3">
       <figcaption>Fig. 1 - Quarterly performance report 2026.</figcaption>
   </figure>
   ```
10. **`<details>` and `<summary>`**: Native disclosure accordion widget without any JavaScript!
    ```html
    <details>
        <summary>What is HTML5?</summary>
        <p>HTML5 is the latest evolution of the standard that defines HTML.</p>
    </details>
    ```
11. **`<mark>`**: Highlights text (mimics yellow highlighter).
12. **`<time>`**: Machine-readable date/time representation.
    ```html
    <time datetime="2026-10-23T11:45">October 23, 2026</time>
    ```
13. **`<meter>` vs `<progress>`**:
    - `<progress>`: Represents task completion (e.g., download 70% finished).
      ```html
      <progress value="70" max="100">70%</progress>
      ```
    - `<meter>`: Represents a scalar gauge within a known range (e.g., disk usage, battery, test score).
      ```html
      <meter min="0" max="100" low="30" high="80" optimum="90" value="85">85%</meter>
      ```

---

## 4. Forms, Input Controls & Validations In-Depth

Forms handle user input and transmission to servers.

```html
<form action="/submit-endpoint" method="POST" enctype="multipart/form-data" novalidate>
    <!-- Fieldset & Legend for grouping -->
    <fieldset>
        <legend>Personal Information</legend>

        <!-- 1. Text Input with Label -->
        <label for="username">Full Name:</label>
        <input type="text" id="username" name="username" placeholder="e.g. Rahul Sharma"
               required minlength="3" maxlength="30" autofocus>

        <!-- 2. Email Input with built-in validation -->
        <label for="usermail">Email Address:</label>
        <input type="email" id="usermail" name="email" required autocomplete="email">

        <!-- 3. Password Input -->
        <label for="pwd">Password:</label>
        <input type="password" id="pwd" name="password" required minlength="8">

        <!-- 4. Number Input with min, max, step -->
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" min="18" max="99" step="1" value="21">

        <!-- 5. Date Input -->
        <label for="dob">Date of Birth:</label>
        <input type="date" id="dob" name="dob" min="1950-01-01" max="2026-12-31">

        <!-- 6. File Upload (requires enctype="multipart/form-data") -->
        <label for="resume">Upload Resume (PDF only):</label>
        <input type="file" id="resume" name="resume" accept=".pdf" multiple>

        <!-- 7. Radio Buttons (Same 'name' groups them so only one is selectable) -->
        <p>Gender:</p>
        <input type="radio" id="male" name="gender" value="male" checked>
        <label for="male">Male</label>
        <input type="radio" id="female" name="gender" value="female">
        <label for="female">Female</label>

        <!-- 8. Checkboxes (Independent toggles) -->
        <p>Skills:</p>
        <input type="checkbox" id="skill_html" name="skills" value="HTML" checked>
        <label for="skill_html">HTML5</label>
        <input type="checkbox" id="skill_css" name="skills" value="CSS">
        <label for="skill_css">CSS3</label>

        <!-- 9. Select Dropdown with Optgroup -->
        <label for="city">Choose City:</label>
        <select id="city" name="city" required>
            <option value="" disabled selected>-- Select City --</option>
            <optgroup label="Maharashtra">
                <option value="mumbai">Mumbai</option>
                <option value="pune">Pune</option>
            </optgroup>
            <optgroup label="Karnataka">
                <option value="bangalore">Bengaluru</option>
            </optgroup>
        </select>

        <!-- 10. Datalist (Autocomplete search input) -->
        <label for="browser_choice">Preferred Browser:</label>
        <input list="browsers" id="browser_choice" name="browser">
        <datalist id="browsers">
            <option value="Google Chrome">
            <option value="Mozilla Firefox">
            <option value="Brave">
            <option value="Microsoft Edge">
        </datalist>

        <!-- 11. Range Slider -->
        <label for="experience">Experience (Years):</label>
        <input type="range" id="experience" name="exp" min="0" max="20" value="3">

        <!-- 12. Textarea -->
        <label for="comments">Bio / Comments:</label>
        <textarea id="comments" name="comments" rows="4" cols="40" placeholder="Tell us about yourself..."></textarea>

        <!-- Buttons -->
        <button type="submit">Submit Form</button>
        <button type="reset">Reset Form</button>
    </fieldset>
</form>
```

---

## 5. Regex (Pattern Validation) in HTML Forms

The `pattern` attribute uses standard JavaScript regular expressions to validate user input prior to form submission.

### Regular Expression Symbols Cheat Sheet:
- `\d` or `[0-9]`: Any digit
- `[a-z]`: Any lowercase letter
- `[A-Z]`: Any uppercase letter
- `[a-zA-Z0-9]`: Any alphanumeric character
- `^`: Start of string
- `$`: End of string
- `+`: 1 or more occurrences
- `*`: 0 or more occurrences
- `{min,max}`: Minimum and maximum number of occurrences
- `[^...]`: Negation (matches anything NOT inside brackets)

### Common Validation Patterns for Practical Labs & Exams:

1. **Indian 10-Digit Mobile Number (starting with 6, 7, 8, or 9)**:
   ```html
   <input type="tel" name="phone" pattern="[6-9][0-9]{9}" title="Enter valid 10-digit mobile number starting with 6, 7, 8, or 9">
   ```

2. **Full Name (5 to 10 characters only, letters only)**:
   ```html
   <input type="text" name="fname" pattern="[a-zA-Z\s]{5,10}" title="Name must be between 5 and 10 letters">
   ```

3. **Strong Password (at least 8 chars, 1st char uppercase, followed by alphanumerics)**:
   ```html
   <input type="password" name="password" pattern="[A-Z][a-zA-Z0-9]{7,}" title="Password must start with capital letter and be at least 8 characters long">
   ```

4. **Specific Pattern (First uppercase, 2 small letters, ends with a special symbol)**:
   ```html
   <input type="text" name="code" pattern="[A-Z][a-z]{2}[^a-zA-Z0-9]" title="1 Capital, 2 Small, 1 Special Symbol">
   ```

5. **Indian PAN Card Number (5 uppercase letters + 4 digits + 1 uppercase letter)**:
   ```html
   <input type="text" name="pan" pattern="[A-Z]{5}[0-9]{4}[A-Z]{1}" title="Format: ABCDE1234F">
   ```

6. **Indian PIN Code (6 digits, cannot start with 0)**:
   ```html
   <input type="text" name="pincode" pattern="[1-9][0-9]{5}" title="Enter 6-digit postal PIN code">
   ```

---

## 6. HTTP Methods in Forms (GET vs POST)

| Feature | GET Method | POST Method |
|---|---|---|
| **Data Transmission** | Appended to URL as query string (`?key=val&k2=v2`) | Sent inside the HTTP Request Body |
| **Data Visibility** | Fully visible in the browser address bar | Hidden from URL bar |
| **Security** | ❌ Not secure for passwords, tokens, private data | ✅ Secure (especially with HTTPS/SSL) |
| **Data Length** | Limited (usually ~2048 characters depending on browser) | Virtually unlimited |
| **Bookmarkable / History**| ✅ Yes, can be bookmarked and cached | ❌ No, cannot be bookmarked without resubmitting |
| **Best Used For** | Search queries, filtering, read-only requests | Passwords, file uploads, transactions, registrations |

---

## 7. Tables & Data Presentation

Tables must use semantic structure (`<thead>`, `<tbody>`, `<tfoot>`) and accessibility headers (`scope="col|row"`).

```html
<table border="1" cellpadding="8" cellspacing="0">
    <caption>Employee Performance 2026</caption>
    <thead>
        <tr>
            <th scope="col">ID</th>
            <th scope="col">Name</th>
            <th scope="col">Department</th>
            <th scope="col" colspan="2">Contact Info</th> <!-- Spans 2 columns -->
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>101</td>
            <td>Aman Verma</td>
            <td rowspan="2">Engineering</td> <!-- Spans 2 rows -->
            <td>aman@mail.com</td>
            <td>+91 9876543210</td>
        </tr>
        <tr>
            <td>102</td>
            <td>Pooja Hegde</td>
            <td>pooja@mail.com</td>
            <td>+91 9876543211</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="5" style="text-align: center;">Total Active Employees: 2</td>
        </tr>
    </tfoot>
</table>
```

---

## 8. Embedded Media

### Native Audio & Video
```html
<!-- Video with fallback and controls -->
<video width="640" height="360" controls poster="thumbnail.jpg" preload="metadata">
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.webm" type="video/webm">
    <track src="subtitles_en.vtt" kind="subtitles" srclang="en" label="English">
    Your browser does not support the video tag.
</video>

<!-- Audio -->
<audio controls autoplay muted loop>
    <source src="podcast.mp3" type="audio/mpeg">
    <source src="podcast.ogg" type="audio/ogg">
    Your browser does not support the audio element.
</audio>
```

### Responsive Images with `<picture>` & `srcset`
```html
<picture>
    <source media="(min-width: 1024px)" srcset="large-banner.jpg">
    <source media="(min-width: 600px)" srcset="medium-banner.jpg">
    <img src="small-banner.jpg" alt="Company Tech Conference" loading="lazy">
</picture>
```

---

## 9. Web Storage, SEO & Accessibility

### Client-Side Storage Comparison
| Storage Type | Capacity | Lifetime | Sent to Server? | Access Scope |
|---|---|---|---|---|
| **Cookies** | ~4 KB | Configurable with expiry date | ✅ Sent with every HTTP request | Accessible via JS / HTTP-only |
| **LocalStorage** | ~5-10 MB | Permanent until cleared manually | ❌ Stored strictly on client | Same origin (domain + port) |
| **SessionStorage**| ~5-10 MB | Cleared as soon as browser tab is closed | ❌ Stored strictly on client | Specific to current tab |

### Basic ARIA (Accessible Rich Internet Applications)
- `aria-label`: Provides invisible description for screen readers (`<button aria-label="Close menu">X</button>`)
- `role`: Overrides element purpose (`<div role="button" tabindex="0">Click me</div>`)
- `aria-hidden="true"`: Hides purely decorative icons from screen readers.

---

## 10. Cheat Sheet & Quick Reference

1. Always add `alt="..."` to `<img>` for accessibility & SEO.
2. Always pair `<label for="inputId">` with `<input id="inputId">`.
3. Use `loading="lazy"` on images and iframes below the fold to speed up page loads.
4. Always wrap tabular headers in `<th>` inside `<thead>`.
5. Use `<button type="button">` inside forms when triggering JS so it doesn't accidentally trigger form submission!
