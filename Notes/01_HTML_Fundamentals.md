# HTML: Fundamentals & Web Architecture

---

## 1. Introduction to HTML

**HTML** stands for **HyperText Markup Language**. It is the standard markup language used to structure web documents, enabling web browsers to interpret and render text, images, and other media into visual, interactive web pages.

### Deconstructing the Name:
* **HyperText:** Text that contains references or hyperlinks to other documents, resources, or web pages, allowing users to navigate non-linearly across the web.
  ```html
  <a href="about.html">About Us</a>
  ```
* **Markup (Text + Structure/Information):** A system of tags and annotations added to raw text to describe its structure, meaning, and presentation format.
  ```html
  <h3>...What a Life...</h3>
  <button>Click to change</button>
  ```
* **Language:** A standardized syntax comprising predefined elements, tags, attributes, and semantic rules that web browsers recognize and follow.

---

## 2. Key Advantages of HTML

| Advantage | Description |
| :--- | :--- |
| **Simple & Easy to Learn** | Features an intuitive, tag-based declarative syntax. |
| **Defines Page Structure** | Provides the architectural skeleton for web pages (`<header>`, `<nav>`, `<main>`, `<footer>`, etc.). |
| **Multimedia & Hyperlink Support** | Easily embeds external resources such as images, audio, video, and hyperlinks. |
| **CSS & JavaScript Integration** | Pairs seamlessly with CSS (for styling and layouts) and JavaScript (for interactivity and logic). |
| **Platform Independent** | Runs across different operating systems (Windows, macOS, Linux, Android, iOS) without modification. |
| **Universal Browser Support** | Supported by all modern web browsers (Chrome, Edge, Firefox, Safari, Opera). |
| **Forms & User Inputs** | Built-in elements for collecting user data (text inputs, checkboxes, radio buttons, file uploads). |
| **Semantic HTML** | Elements describe their own meaning to both browsers and assistive devices, boosting accessibility. |
| **SEO Friendly** | Well-structured markup helps search engine crawlers understand and index page content accurately. |
| **Backend Agnostic** | Integrates easily with any backend technology or web server (Node.js, Python, Java, PHP, Go, etc.). |
| **Open Standard** | Maintained and governed by standard bodies (WHATWG and W3C) as a free, open technology. |

---

## 3. HTML vs. Programming Languages

HTML is a **markup language**, not a programming language.

| Feature | HTML (Markup Language) | Programming Languages (e.g., Python, Java, C++) |
| :--- | :--- | :--- |
| **Purpose** | Defines the structure and presentation of content. | Defines business logic, data operations, and system behavior. |
| **Logic Support** | No computational logic (no `if/else`, loops, or math). | Full support for conditionals, loops, functions, and algorithms. |
| **Variables & State** | Does not support variables or data storage natively. | Supports variables, data structures, and memory management. |
| **Execution** | Parsed and rendered visually by a browser engine. | Compiled to machine code/bytecode or executed by an interpreter. |
| **Error Handling** | Fault-tolerant (browsers attempt to render even invalid markup). | Strict (syntax or runtime errors break execution or raise exceptions). |

---

## 4. How HTML Works Internally (Browser Rendering Pipeline)

HTML is a **declarative language**: you specify *what* content exists (e.g., `<h4>Hello Guys</h4>` defines a fourth-level heading), and the browser engine determines *how* to parse, style, and paint it on screen.

### Critical Rendering Path (CRP)

```text
[ Raw HTML Bytes ]
       │
       ▼
[ Tokenize & Parse ] ──> Builds: DOM Tree (Document Object Model)
       │
       ├───> [ Parse CSS ] ──> Builds: CSSOM Tree (CSS Object Model)
       │          │
       │          ▼
       ├───> [ Execute JavaScript ] ──> (Can read/modify DOM & CSSOM)
       │          │
       │          ▼
       └───> [ Build Render Tree ] ──── (Combines visible DOM + CSSOM nodes)
                  │
                  ▼
             [ Layout (Reflow) ] ────── (Calculates exact geometry & positions)
                  │
                  ▼
             [ Paint & Composite ] ─── (Fills pixels, blends layers)
                  │
                  ▼
            [ Screen Display ]
```

1. **DOM Tree Creation:** The browser turns raw HTML bytes into characters, tokens, and finally a hierarchical tree of nodes known as the **DOM (Document Object Model)**.
2. **CSSOM Tree Creation:** CSS rules are parsed into the **CSSOM (CSS Object Model)** tree.
3. **Render Tree:** The browser combines the DOM and CSSOM trees into a **Render Tree**, omitting elements that are not visible (e.g., `<head>` or elements with `display: none`).
4. **Layout (Reflow):** Computes the exact geometric dimensions and screen position for each visible element.
5. **Paint & Composite:** Rasterizes pixels onto the screen and composites overlapping layers for final display.

---

## 5. Anatomy of an HTML Document

A valid, standard HTML5 document follows this baseline template:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First Web Page</title>
  </head>
  <body>
    <h1>Hello World</h1>
    <p>This is my first web document.</p>
  </body>
</html>
```

### Essential Tags Explained

* `<!DOCTYPE html>`: **Document Type Declaration**. It must be the very first line of any HTML file. It tells the browser that the document adheres to modern **HTML5** standards and ensures standard rendering mode (preventing quirks mode).
* `<html lang="en">`: The **root element** enclosing all other HTML elements. The `lang` attribute declares the primary language of the document.
* `<head>`: Contains **metadata**, configuration settings, character encoding definitions (`UTF-8`), viewport settings for responsive design, and links to external resources (stylesheets, fonts). Content inside `<head>` is not rendered directly in the web page body.
* `<title>`: Sets the title displayed on the browser tab, bookmarks, and search engine results.
* `<body>`: Represents the document's main container. All visible content (text, images, links, forms) resides within this tag.
* `<h1>` to `<h6>`: **Heading elements** representing 6 levels of document hierarchy:
  * `<h1>` is the primary, highest-level heading (used once per page for SEO and clarity).
  * `<h6>` is the lowest-level subheading.
* `<p>`: The **paragraph element**, used to structure blocks of readable text.
* `<a>`: The **anchor element**, used to create hyperlinks (`href` specifies the destination URL).
* `<button>`: An interactive button element used to trigger user actions or JavaScript events.

---

## 6. Web Fundamentals & Homework Concepts

### 1. Client
A **Client** is any hardware device or software application (such as a laptop running a web browser or a smartphone running an app) that requests resources, data, or services from a server over a network.

### 2. Server
A **Server** is a dedicated computer or software program that stores resources (web pages, databases, media files) and listens for incoming requests from clients. When a request arrives, the server processes it and sends back an appropriate response.

### 3. Web Browser
A **Web Browser** is a client-side software application (e.g., Google Chrome, Firefox, Safari, Edge) designed to retrieve resources from web servers, interpret HTML, CSS, and JavaScript, and render them into interactive graphical web pages.

### 4. Browser Engines (Rendering Engines)
The **Browser Engine** is the core internal component of a web browser responsible for parsing HTML and CSS, computing layout geometry, and painting visual pixels onto the screen.

| Engine | Primary Browsers | Developer / Project |
| :--- | :--- | :--- |
| **Blink** | Google Chrome, Microsoft Edge, Brave, Opera, Vivaldi | Google / Chromium Project |
| **Gecko** | Mozilla Firefox | Mozilla Foundation |
| **WebKit** | Apple Safari (and all iOS web browsers) | Apple |

### 5. HTTP (HyperText Transfer Protocol)
**HTTP** is the foundational, application-layer networking protocol of the World Wide Web. It governs how requests and responses are formatted and exchanged between clients and servers. HTTP transmits data as plain text.

### 6. HTTPS (HyperText Transfer Protocol Secure)
**HTTPS** is the secure, encrypted extension of HTTP. It uses **TLS/SSL (Transport Layer Security / Secure Sockets Layer)** encryption to secure communications, protecting sensitive user data (passwords, credit card numbers) against eavesdropping, interception, and tampering.

### 7. WWW (World Wide Web)
The **World Wide Web** (commonly referred to as the Web) is a global information system of interconnected documents and digital resources accessible over the Internet via hyperlinks and URLs using the HTTP/HTTPS protocols.

> **Note:** The *Internet* is the underlying physical network infrastructure connecting computers globally; the *Web* is an information service built on top of the Internet.

### 8. IP Address (Internet Protocol Address)
An **IP Address** is a unique numerical label assigned to every device connected to a computer network that uses the Internet Protocol. It identifies the host and its location on the network.
* **IPv4:** 32-bit numerical address format written in 4 decimal octets (e.g., `192.168.1.1` or `142.250.190.46`).
* **IPv6:** 128-bit hexadecimal address format introduced to replace IPv4 and provide a virtually inexhaustible supply of addresses (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).

### 9. Domain Name
A **Domain Name** is a human-readable alias for a numerical IP address (e.g., `google.com` or `wikipedia.org`). The **DNS (Domain Name System)** translates human-friendly domain names into computer-friendly IP addresses so browsers know where to connect.

### 10. URI vs. URL

* **URI (Uniform Resource Identifier):** An umbrella term for any string of characters that uniquely identifies an abstract or physical resource by name, location, or both.
* **URL (Uniform Resource Locator):** A specific subset of URI that not only identifies the resource, but also specifies *how* and *where* to locate it by defining the access protocol and location.

```text
                  Uniform Resource Identifier (URI)
                ┌───────────────────────────────────┐
                │                                   │
                │     URL (Location + Protocol)     │
                │     https://example.com/page      │
                │                                   │
                │     URN (Name only)               │
                │     urn:isbn:0451450523           │
                └───────────────────────────────────┘
```

* **Key Takeaway:** *All URLs are URIs, but not all URIs are URLs.*
