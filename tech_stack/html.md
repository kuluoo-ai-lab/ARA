# HTML LANGUAGE FORMAL SPECIFICATION
## HyperText Markup Language - Complete Code Generation Standard


## TABLE OF CONTENTS

1. [Executive Summary](#executive-summary)
2. [Language Philosophy](#language-philosophy)
3. [Core Principles](#core-principles)
4. [Lexical Definition](#lexical-definition)
5. [Syntax Definition](#syntax-definition)
6. [Type System](#type-system)
7. [Semantic Structure](#semantic-structure)
8. [12 Primary Keywords](#12-primary-keywords)
9. [Document Structure Rules](#document-structure-rules)
10. [Code Generation Workflow](#code-generation-workflow)
11. [Best Practices & Standards](#best-practices--standards)
12. [Safety & Validation Rules](#safety--validation-rules)

---

## EXECUTIVE SUMMARY

**HTML (HyperText Markup Language)** is a declarative, tag-based, semantic markup language designed to structure content and create accessible web pages with built-in meaning, interactivity, and responsiveness.

### Language Goals

- ✅ **Semantic Clarity:** Use meaningful tags that convey document structure
- ✅ **Accessibility:** 100% WCAG 2.1 AA compliance built-in
- ✅ **Responsive Design:** Mobile-first, device-agnostic markup
- ✅ **SEO Optimization:** Built-in semantic structure for search engines
- ✅ **Interactivity:** Native form handling and user interaction
- ✅ **Performance:** Lightweight, efficient markup compilation
- ✅ **Validation:** Complete W3C compliance checking
- ✅ **Security:** Built-in protection against XSS and injection attacks

### Core Metrics

| Metric | Value |
|--------|-------|
| Parsing Speed | Milliseconds for average document |
| Browser Support | 99%+ across all modern browsers |
| Accessibility Score | WCAG 2.1 AAA capable |
| SEO Performance | Maximum search engine optimization |
| Security Rating | No vulnerabilities when properly written |
| File Size | ~30KB average web page |
| Load Time | <1s on standard connections |

---

## LANGUAGE PHILOSOPHY

### Design Principles

1. **Semantic Over Visual**
   - Structure conveys meaning
   - Presentation handled by CSS
   - Content accessibility prioritized

2. **Progressive Enhancement**
   - Base functionality without CSS/JS
   - Enhanced experience with additional layers
   - Works for all users, all devices

3. **Content First**
   - HTML contains the content
   - Meaning embedded in structure
   - Tags describe, not decorate

4. **Accessibility by Default**
   - WCAG 2.1 compliance built-in
   - ARIA attributes for enhancement
   - Keyboard and screen reader ready

5. **Semantic HTML5**
   - Meaningful tags over generic divs
   - Proper element hierarchy
   - Clear document outline

### Core Values

```
Semantic   > Visual
Accessible > Decorative
Structured > Chaotic
Valid      > Broken
Simple     > Complex
Users      > Preferences
```

---

## CORE PRINCIPLES

### The HTML Generation Paradigm

```
USER INTENT
    ↓
UNDERSTAND REQUIREMENT
    ↓
CHOOSE SEMANTIC TAGS
    ↓
STRUCTURE DOCUMENT
    ↓
ADD ACCESSIBILITY
    ↓
VALIDATE MARKUP
    ↓
OPTIMIZE PERFORMANCE
    ↓
PRODUCTION-READY HTML
```

### Key Characteristics

1. **Tag-Based Declarative Language**
   - Uses `<tag>content</tag>` syntax
   - Tags describe purpose of content
   - Attributes modify tag behavior

2. **Tree Structure**
   - Parent-child hierarchical relationships
   - Proper nesting required
   - Clear document outline

3. **Semantic Elements**
   - Each tag has specific meaning
   - Used for their intended purpose
   - Conveys content structure

4. **Attributes for Enhancement**
   - Modify element behavior
   - Provide additional information
   - Enable interactivity

5. **Content at Core**
   - Text, images, media, forms
   - Users consume content
   - Structure supports content

---

## LEXICAL DEFINITION

### Token Types

#### HTML5 Tag Categories

```
SEMANTIC TAGS (Structural Meaning):
<header>        # Page header or section header
<nav>           # Navigation links
<main>          # Main content area
<article>       # Self-contained article
<section>       # Thematic grouping
<aside>         # Sidebar or related content
<footer>        # Footer of page/section

CONTENT TAGS (Information Display):
<h1> to <h6>   # Headings (hierarchy)
<p>             # Paragraph
<pre>           # Preformatted text
<blockquote>    # Block-level quote
<ul>            # Unordered list
<ol>            # Ordered list
<li>            # List item
<dl>            # Description list
<dt>            # Definition term
<dd>            # Definition description

INLINE TAGS (Text-Level Semantics):
<strong>        # Strong importance
<em>            # Emphasis
<mark>          # Highlighted text
<code>          # Code snippet
<kbd>           # Keyboard input
<samp>          # Sample output
<var>           # Variable
<sub>           # Subscript
<sup>           # Superscript
<small>         # Side comments
<time>          # Date/time
<u>             # Unarticulated annotation
<s>             # Strikethrough

INTERACTIVE TAGS (Forms & User Input):
<form>          # Form container
<input>         # Input field
<textarea>      # Multi-line text input
<select>        # Dropdown menu
<option>        # Option in select
<optgroup>      # Group of options
<button>        # Clickable button
<label>         # Form field label
<fieldset>      # Form field grouping
<legend>        # Fieldset legend

MEDIA TAGS (Multimedia):
<img>           # Image
<picture>       # Responsive image
<source>        # Media source
<audio>         # Audio content
<video>         # Video content
<track>         # Text track for media
<canvas>        # Drawing surface
<svg>           # Scalable vector graphics
<iframe>        # Embedded document

METADATA & STRUCTURE:
<html>          # Document root
<head>          # Document metadata
<title>         # Page title
<meta>          # Metadata
<link>          # External resource
<style>         # CSS styles
<script>        # JavaScript code
<noscript>      # No-script fallback
<base>          # Base URL
<body>          # Document body
```

#### Attributes (Standard)

```
GLOBAL ATTRIBUTES (all elements):
id              # Unique identifier
class           # CSS class names
style           # Inline CSS
title           # Tooltip text
lang            # Language code
data-*          # Custom data
role            # ARIA role
aria-*          # ARIA attributes
hidden          # Hide element
tabindex        # Tab order

COMMON ATTRIBUTES:
href            # Link target
src             # Resource URL
alt             # Alternative text
type            # Element type
name            # Form field name
value           # Field value
placeholder     # Hint text
required        # Field required
disabled        # Field disabled
readonly        # Read-only field
multiple        # Multiple selection
```

#### Special Characters & Entities

```
&lt;            # < (less than)
&gt;            # > (greater than)
&amp;           # & (ampersand)
&quot;          # " (quote)
&apos;          # ' (apostrophe)
&nbsp;          # Non-breaking space
&copy;          # © (copyright)
&reg;           # ® (registered)
&euro;          # € (euro)
&rarr;          # → (right arrow)
&larr;          # ← (left arrow)
```

---

## SYNTAX DEFINITION

### Basic Tag Syntax

#### Tag Structure

```
Opening Tag:     <tagname>
Closing Tag:     </tagname>
Self-Closing:    <tagname />
With Attributes: <tagname attribute="value">

Example:
<p class="intro">This is a paragraph.</p>
```

#### Attribute Syntax

```
Single Attribute:  <tagname attribute="value">
Multiple:          <tagname attr1="val1" attr2="val2">
Boolean:           <input disabled>
Empty Values:      <div data-value="">
```

### Document Structure

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Title</title>
    <link rel="stylesheet" href="styles.css">
  </head>
  <body>
    <header>Header Content</header>
    <nav>Navigation</nav>
    <main>
      <article>Article Content</article>
      <aside>Sidebar</aside>
    </main>
    <footer>Footer</footer>
    <script src="script.js"></script>
  </body>
</html>
```

### Nesting Rules

1. **Proper Nesting Required**
   ```html
   ✅ <p><strong>Bold text</strong></p>
   ❌ <p><strong>Bold text</p></strong>
   ```

2. **Block Elements Stack**
   ```html
   <div>
     <p>First paragraph</p>
     <p>Second paragraph</p>
   </div>
   ```

3. **Inline Elements Flow**
   ```html
   <p>This is <strong>bold</strong> and <em>italic</em>.</p>
   ```

4. **Container Requirements**
   ```html
   <ul>
     <li>Item 1</li>
     <li>Item 2</li>
   </ul>
   ```

---

## TYPE SYSTEM

### Content Types

#### Text Content

```
Plain Text:      Regular text content
Encoded Text:    &lt;escaped&gt; content
Whitespace:      Spaces, tabs, newlines (normalized)
Unicode:         Full UTF-8 support
```

#### Media Content

```
Images:          .jpg, .png, .webp, .svg, .gif
Video:           .mp4, .webm, .ogg, .mov
Audio:           .mp3, .wav, .ogg, .aac
Documents:       .pdf embedded or linked
```

#### Element Categories

```
Block Elements:
<div>, <p>, <h1-h6>, <section>, <article>, <nav>, 
<header>, <footer>, <aside>, <main>, <ul>, <ol>, 
<dl>, <blockquote>, <pre>, <form>, <fieldset>, <table>

Inline Elements:
<span>, <a>, <strong>, <em>, <code>, <img>, <button>,
<input>, <label>, <select>, <textarea>, <small>, <mark>,
<time>, <cite>, <abbr>, <sub>, <sup>

Inline-Block Elements:
<img>, <button>, <input>, <select>, <textarea>
```

#### Attribute Types

```
String:          text content
Number:          integer values
Boolean:         attribute present/absent
URL:             href, src, data attributes
Color:           hex, rgb, color names
Date/Time:       ISO 8601 format
Email:           RFC 5322 format
Phone:           E.164 format
```

---

## SEMANTIC STRUCTURE

### Document Outline Algorithm

```
Every HTML document should have clear outline:

<html>
  ├─ <header>               (Page header)
  ├─ <nav>                  (Navigation)
  ├─ <main>                 (Main content)
  │  ├─ <h1>               (Main heading)
  │  ├─ <article>          (Article 1)
  │  │  ├─ <h2>            (Article heading)
  │  │  └─ Content
  │  ├─ <article>          (Article 2)
  │  │  ├─ <h2>            (Article heading)
  │  │  └─ Content
  │  └─ <aside>            (Sidebar)
  │     ├─ <h2>            (Sidebar heading)
  │     └─ Content
  └─ <footer>               (Page footer)
```

### Semantic Element Hierarchy

#### Content Sectioning

```
<article>       # Self-contained composition
  <h1>          # Article title (1 per article)
  <p>           # Content
  <section>     # Thematic section
    <h2>        # Section heading
    <p>         # Section content
  </section>
</article>

<section>       # Thematic grouping
  <h2>          # Section heading
  <p>           # Content
</section>

<aside>         # Related content
  <h2>          # Aside heading
  <p>           # Tangential content
</aside>
```

#### Content Hierarchy

```
<h1>            # Page main topic (1 per page)
  <h2>          # Major section (under h1)
    <h3>        # Subsection (under h2)
      <h4>      # Sub-subsection
        <h5>    # Minor subdivision
          <h6>  # Smallest heading
```

---

## 12 PRIMARY KEYWORDS

### The 12 Core HTML Keywords

These are the fundamental building blocks of HTML structure and semantics:

#### 1. **DOCUMENT** - Page Structure Foundation

**Purpose:** Defines the root HTML document and its metadata

**Keywords:**
- `<!DOCTYPE html>` - Document type declaration
- `<html>` - Document root element
- `<head>` - Metadata container
- `<body>` - Content container

**Syntax:**
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- Metadata goes here -->
  </head>
  <body>
    <!-- Content goes here -->
  </body>
</html>
```

**Rules:**
- DOCTYPE MUST be first line
- Only one `<html>` per document
- `<head>` before `<body>`
- Always include `lang` attribute
- `<title>` required in `<head>`

**Example:**
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>My Website</title>
  </head>
  <body>
    <h1>Welcome</h1>
  </body>
</html>
```

---

#### 2. **SEMANTIC** - Meaningful Structure Tags

**Purpose:** Convey content meaning and document structure

**Keywords:**
- `<header>` - Header section
- `<nav>` - Navigation section
- `<main>` - Main content
- `<article>` - Self-contained article
- `<section>` - Thematic section
- `<aside>` - Related/sidebar content
- `<footer>` - Footer section

**Syntax:**
```html
<header>
  <h1>Site Title</h1>
  <p>Tagline</p>
</header>

<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>

<main>
  <article>
    <h2>Article Title</h2>
    <p>Content</p>
  </article>
  
  <section>
    <h2>Related Content</h2>
    <p>More content</p>
  </section>
  
  <aside>
    <h3>Sidebar</h3>
    <p>Tangential info</p>
  </aside>
</main>

<footer>
  <p>&copy; 2025 Company</p>
</footer>
```

**Rules:**
- Use semantic elements over generic `<div>`
- One `<main>` per page
- `<header>` and `<footer>` can be per section
- `<nav>` for navigation links only
- Proper nesting required

**Best Practices:**
```html
✅ GOOD:
<article>
  <h2>Article Title</h2>
  <p>Content</p>
</article>

❌ BAD:
<div class="article">
  <div class="title">Article Title</div>
  <div>Content</div>
</div>
```

---

#### 3. **HEADING** - Content Hierarchy

**Purpose:** Establish document outline and structure

**Keywords:**
- `<h1>` - Main heading (1 per page recommended)
- `<h2>` - Major section
- `<h3>` - Subsection
- `<h4>` - Sub-subsection
- `<h5>` - Minor subdivision
- `<h6>` - Smallest heading

**Syntax:**
```html
<h1>Page Main Topic</h1>

<section>
  <h2>Major Section</h2>
  <p>Content</p>
  
  <h3>Subsection</h3>
  <p>More content</p>
  
  <h4>Sub-subsection</h4>
  <p>Detailed content</p>
</section>
```

**Rules:**
- Never skip heading levels (h1 to h3 bad, h1 to h2 good)
- One `<h1>` per page (preferred)
- Follow logical hierarchy
- Use for structure, not styling

**Example - Document Outline:**
```
Page Outline:
├─ h1: "Welcome to My Blog"
├─ h2: "Latest Articles"
│  ├─ h3: "Article 1 Title"
│  └─ h3: "Article 2 Title"
└─ h2: "About Me"
   └─ h3: "My Background"
```

---

#### 4. **CONTENT** - Text & Information Display

**Purpose:** Mark up and present content properly

**Keywords:**
- `<p>` - Paragraph
- `<pre>` - Preformatted text
- `<blockquote>` - Block quote
- `<hr>` - Thematic break
- `<br>` - Line break
- `<figure>` - Self-contained illustration
- `<figcaption>` - Caption for figure
- `<code>` - Code snippet
- `<ul>` - Unordered list
- `<ol>` - Ordered list
- `<li>` - List item
- `<dl>` - Description list
- `<dt>` - Definition term
- `<dd>` - Definition description

**Syntax:**
```html
<p>Regular paragraph with text.</p>

<blockquote cite="https://example.com">
  <p>This is a quote from a source.</p>
</blockquote>

<pre><code>function hello() {
  console.log("Hello World");
}</code></pre>

<figure>
  <img src="image.jpg" alt="Description">
  <figcaption>Photo by John Doe</figcaption>
</figure>

<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<ol>
  <li>First step</li>
  <li>Second step</li>
</ol>

<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language</dd>
  <dt>CSS</dt>
  <dd>Cascading Style Sheets</dd>
</dl>
```

**Rules:**
- One topic per paragraph
- Use semantic lists over styled divs
- Use `<pre>` with `<code>` for code blocks
- Proper list nesting required
- `<blockquote>` for substantial quotes

---

#### 5. **INLINE** - Text-Level Semantics

**Purpose:** Mark up text with semantic meaning

**Keywords:**
- `<strong>` - Strong importance
- `<em>` - Emphasized text
- `<mark>` - Highlighted text
- `<small>` - Side comments
- `<cite>` - Citation
- `<abbr>` - Abbreviation
- `<time>` - Date/time
- `<code>` - Code
- `<kbd>` - Keyboard input
- `<var>` - Variable
- `<sub>` - Subscript
- `<sup>` - Superscript
- `<u>` - Unarticulated annotation
- `<s>` - Strikethrough

**Syntax:**
```html
<p>This is <strong>very important</strong> text.</p>

<p>This is <em>emphasized</em> content.</p>

<p>Use <mark>this technique</mark> for best results.</p>

<p>The chemical formula is H<sub>2</sub>O.</p>

<p>Press <kbd>Ctrl+C</kbd> to copy.</p>

<p>Abbr: <abbr title="HyperText Markup Language">HTML</abbr></p>

<p>The event is <time datetime="2025-12-31">December 31</time>.</p>

<p>Use the <code>console.log()</code> function.</p>
```

**Rules:**
- Use semantic tags for meaning, not appearance
- `<strong>` for importance, `<em>` for stress
- Don't use for styling (use CSS instead)
- Proper nesting within inline context

---

#### 6. **LINK** - Navigation & Resource References

**Purpose:** Connect pages and resources

**Keywords:**
- `<a>` - Hyperlink (anchor)
- `<link>` - External resource
- `<base>` - Base URL
- `href` - Link target
- `target` - Link behavior
- `rel` - Relationship
- `type` - Resource type

**Syntax:**
```html
<!-- Basic link -->
<a href="/about">About Us</a>

<!-- Link to external site -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
  Example
</a>

<!-- Link with title -->
<a href="/contact" title="Contact our team">Contact</a>

<!-- Email link -->
<a href="mailto:info@example.com">Email Us</a>

<!-- Phone link -->
<a href="tel:+1-555-0123">Call Us</a>

<!-- Document download -->
<a href="/files/document.pdf" download>Download PDF</a>

<!-- Skip link (accessibility) -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<!-- Link tag in head -->
<link rel="stylesheet" href="styles.css">
<link rel="icon" href="favicon.ico">
<link rel="canonical" href="https://example.com/page">
```

**Rules:**
- Use descriptive link text
- Include `title` for additional context
- Use `rel="noopener noreferrer"` for `target="_blank"`
- Never open in new tab by default
- Use meaningful href values

**Accessibility Rules:**
```html
❌ BAD: <a href="/page">Click here</a>
✅ GOOD: <a href="/page">Our services page</a>

❌ BAD: <a href="https://external.com">Link</a>
✅ GOOD: <a href="https://external.com" target="_blank" rel="noopener noreferrer">
  External site
</a>
```

---

#### 7. **IMAGE** - Visual Content & Media

**Purpose:** Embed images and visual media responsively

**Keywords:**
- `<img>` - Image element
- `<picture>` - Responsive image container
- `<source>` - Media source
- `src` - Image source
- `alt` - Alternative text
- `srcset` - Responsive sources
- `sizes` - Responsive sizes

**Syntax:**
```html
<!-- Basic image -->
<img src="photo.jpg" alt="Descriptive alt text" width="400" height="300">

<!-- Responsive image with srcset -->
<img src="photo.jpg" 
     srcset="photo-small.jpg 400w, 
             photo-medium.jpg 800w,
             photo-large.jpg 1200w"
     sizes="(max-width: 600px) 400px,
            (max-width: 1200px) 800px,
            1200px"
     alt="Descriptive alt text">

<!-- Picture element for art direction -->
<picture>
  <source media="(min-width: 1200px)" srcset="large.jpg">
  <source media="(min-width: 600px)" srcset="medium.jpg">
  <img src="small.jpg" alt="Descriptive text">
</picture>

<!-- Decorative image -->
<img src="decorative.png" alt="" aria-hidden="true">

<!-- Image in figure -->
<figure>
  <img src="chart.png" alt="Sales data chart">
  <figcaption>Q4 sales by region</figcaption>
</figure>
```

**Rules:**
- Always include descriptive `alt` text
- Use `alt=""` only for purely decorative images
- Include `width` and `height` to prevent layout shift
- Use `srcset` for responsive images
- Use `<picture>` for art direction
- Optimize image files before embedding
- Use modern formats (WebP with fallback)

**Alt Text Guidelines:**
```html
❌ BAD:
<img src="image.jpg" alt="image">
<img src="photo.jpg" alt="photo">

✅ GOOD:
<img src="sunset.jpg" alt="Sunset over the Pacific Ocean">
<img src="team.jpg" alt="Marketing team at annual conference">
```

---

#### 8. **FORM** - User Input & Interaction

**Purpose:** Collect user data securely and accessibly

**Keywords:**
- `<form>` - Form container
- `<input>` - Input field
- `<textarea>` - Text area
- `<select>` - Dropdown menu
- `<option>` - Menu option
- `<optgroup>` - Option group
- `<button>` - Button
- `<label>` - Field label
- `<fieldset>` - Field grouping
- `<legend>` - Fieldset title
- `<datalist>` - Input suggestions
- `<output>` - Calculation result

**Syntax:**
```html
<form action="/submit" method="POST" novalidate>
  <!-- Text input with label -->
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" required>
  
  <!-- Email input -->
  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required>
  
  <!-- Password -->
  <label for="password">Password:</label>
  <input type="password" id="password" name="password" required minlength="8">
  
  <!-- Textarea -->
  <label for="message">Message:</label>
  <textarea id="message" name="message" rows="5" required></textarea>
  
  <!-- Select dropdown -->
  <label for="country">Country:</label>
  <select id="country" name="country" required>
    <option value="">-- Select --</option>
    <optgroup label="North America">
      <option value="us">United States</option>
      <option value="ca">Canada</option>
    </optgroup>
  </select>
  
  <!-- Radio buttons -->
  <fieldset>
    <legend>Choose an option:</legend>
    <label>
      <input type="radio" name="option" value="1"> Option 1
    </label>
    <label>
      <input type="radio" name="option" value="2"> Option 2
    </label>
  </fieldset>
  
  <!-- Checkboxes -->
  <fieldset>
    <legend>Select interests:</legend>
    <label>
      <input type="checkbox" name="interest" value="sports"> Sports
    </label>
    <label>
      <input type="checkbox" name="interest" value="music"> Music
    </label>
  </fieldset>
  
  <!-- Datalist -->
  <label for="browser">Browser:</label>
  <input list="browsers" id="browser" name="browser">
  <datalist id="browsers">
    <option value="Chrome">
    <option value="Firefox">
    <option value="Safari">
  </datalist>
  
  <!-- Buttons -->
  <button type="submit">Submit</button>
  <button type="reset">Clear</button>
  <button type="button">Cancel</button>
</form>
```

**Input Types:**
```html
text, email, password, number, tel, url, date, time,
datetime-local, month, week, color, range, file,
hidden, checkbox, radio, search, button, reset, submit
```

**Rules:**
- Every input needs a `<label>`
- Use `for` attribute to connect label to input
- Include validation attributes (required, minlength, pattern)
- Use semantic input types
- Group related fields with `<fieldset>`
- Always have submit button
- Use `method="POST"` for sensitive data
- Include CSRF protection token

---

#### 9. **TABLE** - Tabular Data

**Purpose:** Display structured tabular data properly

**Keywords:**
- `<table>` - Table container
- `<thead>` - Table header section
- `<tbody>` - Table body section
- `<tfoot>` - Table footer section
- `<tr>` - Table row
- `<th>` - Header cell
- `<td>` - Data cell
- `<caption>` - Table caption
- `<colgroup>` - Column grouping

**Syntax:**
```html
<table>
  <caption>Monthly Sales Report</caption>
  
  <colgroup>
    <col style="width: 30%">
    <col style="width: 23.3%">
    <col style="width: 23.3%">
    <col style="width: 23.3%">
  </colgroup>
  
  <thead>
    <tr>
      <th scope="col">Month</th>
      <th scope="col">Q1</th>
      <th scope="col">Q2</th>
      <th scope="col">Q3</th>
    </tr>
  </thead>
  
  <tbody>
    <tr>
      <th scope="row">Sales</th>
      <td>$10,000</td>
      <td>$12,000</td>
      <td>$15,000</td>
    </tr>
    <tr>
      <th scope="row">Expenses</th>
      <td>$7,000</td>
      <td>$8,000</td>
      <td>$9,000</td>
    </tr>
  </tbody>
  
  <tfoot>
    <tr>
      <th scope="row">Total</th>
      <td>$3,000</td>
      <td>$4,000</td>
      <td>$6,000</td>
    </tr>
  </tfoot>
</table>
```

**Rules:**
- Only use tables for tabular data
- Never use for layout
- Include `<thead>`, `<tbody>`, `<tfoot>`
- Use `<th>` with `scope` attribute for accessibility
- Include `<caption>` describing the table
- Use proper nesting

**Accessibility:**
```html
✅ GOOD:
<th scope="col">Header</th>    <!-- Column header -->
<th scope="row">Header</th>    <!-- Row header -->

❌ BAD:
<td>Header</td>               <!-- Wrong: data cell -->
<th>Header without scope</th> <!-- Wrong: no scope -->
```

---

#### 10. **MEDIA** - Audio, Video & Interactive Content

**Purpose:** Embed and control multimedia content

**Keywords:**
- `<audio>` - Audio content
- `<video>` - Video content
- `<track>` - Text track
- `<source>` - Media source
- `<canvas>` - Drawing surface
- `<svg>` - Vector graphics
- `<iframe>` - Embedded document
- `<embed>` - External content
- `<object>` - Object container

**Syntax:**
```html
<!-- Audio with controls -->
<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
  <source src="audio.ogg" type="audio/ogg">
  Your browser doesn't support HTML5 audio.
</audio>

<!-- Video with controls and captions -->
<video controls width="640" height="360" poster="poster.jpg">
  <source src="video.mp4" type="video/mp4">
  <source src="video.webm" type="video/webm">
  <track src="captions.vtt" kind="captions" srclang="en" label="English">
  Your browser doesn't support HTML5 video.
</video>

<!-- Canvas for drawing -->
<canvas id="myCanvas" width="400" height="300">
  Your browser doesn't support HTML5 canvas.
</canvas>

<!-- SVG graphics -->
<svg width="100" height="100" viewBox="0 0 100 100">
  <circle cx="50" cy="50" r="40" fill="blue" />
</svg>

<!-- Iframe for embedded content -->
<iframe width="560" height="315" 
        src="https://www.youtube.com/embed/dQw4w9WgXcQ"
        title="YouTube video player"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen>
</iframe>
```

**Rules:**
- Always provide multiple `<source>` formats
- Use `controls` attribute for media players
- Include `<track>` for captions/subtitles
- Specify `width` and `height`
- Include fallback content
- Use `poster` attribute for video preview
- Accessibility: captions and transcripts required

---

#### 11. **META** - Document Metadata & Configuration

**Purpose:** Provide document information and configuration

**Keywords:**
- `<meta>` - Metadata
- `<title>` - Document title
- `<style>` - CSS styles
- `<script>` - JavaScript code
- `<link>` - External resources
- `<base>` - Base URL
- `charset` - Character encoding
- `viewport` - Responsive configuration
- `description` - Page description
- `keywords` - SEO keywords
- `author` - Document author
- `og:` - Open Graph metadata

**Syntax:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- Character encoding -->
  <meta charset="UTF-8">
  
  <!-- Viewport for responsive design -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <!-- Page title (shown in browser tab) -->
  <title>Page Title - Website</title>
  
  <!-- Meta description (shown in search results) -->
  <meta name="description" content="Page description for search engines">
  
  <!-- Author -->
  <meta name="author" content="John Doe">
  
  <!-- Keywords (less important now) -->
  <meta name="keywords" content="html, css, javascript">
  
  <!-- Theme color -->
  <meta name="theme-color" content="#3498db">
  
  <!-- Open Graph for social sharing -->
  <meta property="og:title" content="Page Title">
  <meta property="og:description" content="Description">
  <meta property="og:image" content="https://example.com/image.jpg">
  <meta property="og:url" content="https://example.com/page">
  <meta property="og:type" content="website">
  
  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Page Title">
  <meta name="twitter:description" content="Description">
  <meta name="twitter:image" content="https://example.com/image.jpg">
  
  <!-- Favicon -->
  <link rel="icon" href="/favicon.ico">
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">
  
  <!-- Canonical URL -->
  <link rel="canonical" href="https://example.com/page">
  
  <!-- External stylesheet -->
  <link rel="stylesheet" href="styles.css">
  
  <!-- Inline styles -->
  <style>
    body { font-family: sans-serif; }
  </style>
</head>
<body>
  <!-- Content -->
  
  <!-- External script -->
  <script src="script.js"></script>
  
  <!-- Inline script -->
  <script>
    console.log("Hello World");
  </script>
</body>
</html>
```

**Rules:**
- `charset="UTF-8"` must be early in `<head>`
- Always include responsive viewport meta tag
- `<title>` unique and descriptive per page
- Meta description 150-160 characters
- Use Open Graph for social sharing
- Canonical URL prevents duplicate content
- Scripts at end of body (before closing tag)

---

#### 12. **ACCESSIBILITY** - Inclusive & Usable for All

**Purpose:** Ensure content is accessible to all users

**Keywords:**
- `aria-*` - ARIA attributes
- `role` - Element role
- `aria-label` - Accessible label
- `aria-labelledby` - Label reference
- `aria-describedby` - Description
- `aria-hidden` - Hide from screen readers
- `aria-expanded` - Toggle state
- `alt` - Image alternative text
- `title` - Element title
- `lang` - Language attribute

**Syntax:**
```html
<!-- Landmark roles -->
<header role="banner">
  <h1>Site Title</h1>
</header>

<nav aria-label="Main navigation">
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>

<main role="main">
  <!-- Main content -->
</main>

<aside aria-label="Sidebar">
  <!-- Sidebar content -->
</aside>

<footer role="contentinfo">
  <p>&copy; 2025 Company</p>
</footer>

<!-- Skip link -->
<a href="#main" class="skip-link">Skip to main content</a>

<!-- Icon button with accessible label -->
<button aria-label="Close menu">
  <span aria-hidden="true">&times;</span>
</button>

<!-- Expandable section -->
<button aria-expanded="false" aria-controls="menu">
  Menu
</button>
<div id="menu" hidden>
  Menu content
</div>

<!-- Alert region -->
<div role="alert" aria-live="assertive">
  This is an important message
</div>

<!-- Form accessibility -->
<label for="name">Name:</label>
<input id="name" type="text" aria-describedby="name-hint">
<span id="name-hint">Your full name</span>

<!-- Keyboard navigation -->
<button tabindex="0">Click me</button>
<a href="/" tabindex="1">Link</a>

<!-- Language specification -->
<html lang="en">
  <p>English text</p>
  <p lang="es">Texto en español</p>
</html>
```

**Accessibility Checklist:**
```
✅ Semantic HTML used properly
✅ All images have descriptive alt text
✅ Color not sole means of information
✅ Forms properly labeled
✅ Keyboard navigation supported
✅ Screen reader compatible
✅ Contrast ratio meets WCAG AA (4.5:1)
✅ Text resizable without loss of function
✅ Links have clear purpose
✅ No auto-playing audio/video
✅ Language attribute included
✅ Captions for video content
✅ Focus indicators visible
✅ Landmarks defined
```

**WCAG 2.1 Principles:**
```
1. PERCEIVABLE - Information must be perceivable
   • Alternative text for images
   • Captions for audio/video
   • Adaptable content
   • Distinguishable elements

2. OPERABLE - Users must be able to operate
   • Keyboard accessible
   • Enough time for interactions
   • Seizure prevention
   • Navigable

3. UNDERSTANDABLE - Content must be understandable
   • Readable language
   • Predictable behavior
   • Input assistance
   • Readable text

4. ROBUST - Compatible with assistive technologies
   • Valid HTML
   • ARIA attributes
   • Role and state
   • Name, role, value
```

---

## DOCUMENT STRUCTURE RULES

### Complete Valid HTML Document

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- CHARACTER ENCODING (FIRST) -->
  <meta charset="UTF-8">
  
  <!-- VIEWPORT (RESPONSIVE) -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  
  <!-- TITLE (REQUIRED) -->
  <title>Page Title - Website</title>
  
  <!-- DESCRIPTION -->
  <meta name="description" content="Page description">
  
  <!-- FAVICON -->
  <link rel="icon" href="/favicon.ico">
  
  <!-- STYLES -->
  <link rel="stylesheet" href="styles.css">
  <style>
    /* Critical CSS */
  </style>
  
  <!-- PRECONNECT FOR PERFORMANCE -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
</head>

<body>
  <!-- SKIP LINK (ACCESSIBILITY) -->
  <a href="#main" class="skip-link">Skip to main content</a>
  
  <!-- HEADER -->
  <header role="banner">
    <h1>Site Title</h1>
  </header>
  
  <!-- NAVIGATION -->
  <nav aria-label="Main navigation" role="navigation">
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
      <li><a href="/contact">Contact</a></li>
    </ul>
  </nav>
  
  <!-- MAIN CONTENT -->
  <main id="main" role="main">
    <section>
      <h2>Section Heading</h2>
      <p>Content here</p>
    </section>
  </main>
  
  <!-- SIDEBAR (OPTIONAL) -->
  <aside aria-label="Sidebar" role="complementary">
    <h3>Related Links</h3>
    <ul>
      <li><a href="#">Link 1</a></li>
      <li><a href="#">Link 2</a></li>
    </ul>
  </aside>
  
  <!-- FOOTER -->
  <footer role="contentinfo">
    <p>&copy; 2025 Company. All rights reserved.</p>
  </footer>
  
  <!-- SCRIPTS (AT END) -->
  <script src="script.js"></script>
</body>
</html>
```

### Validation Rules

1. **DOCTYPE Declaration**
   - MUST be first line
   - MUST be `<!DOCTYPE html>`

2. **Root Element**
   - `<html>` element wraps all content
   - MUST include `lang` attribute
   - Example: `<html lang="en">`

3. **Head Section**
   - `<meta charset="UTF-8">` first
   - `<title>` required
   - All metadata before closing `</head>`

4. **Body Section**
   - Contains all visible content
   - Semantic structure required
   - Proper nesting essential

5. **Nesting Rules**
   - All tags properly closed
   - No overlapping tags
   - Inline elements inside block elements acceptable
   - Block elements inside inline elements not allowed

---

## CODE GENERATION WORKFLOW

### 6-Step HTML Generation Process

#### STEP-1: UNDERSTAND PROJECT INTENT

**Objective:** Clarify what the HTML page needs to accomplish

```
Questions to Answer:
✓ What is the page purpose?
✓ Who are the users?
✓ What content needs to be displayed?
✓ What interactions are needed?
✓ What devices must it support?
✓ What accessibility standards apply?
✓ What are the performance requirements?
```

**Example:**
```
Project: Create a product landing page
Purpose: Sell a software product
Users: Business decision makers, technical leads
Content: Hero section, features, pricing, testimonials, CTA
Interactions: Form submission, pricing toggle
Devices: Mobile, tablet, desktop
Accessibility: WCAG 2.1 AA
Performance: Lighthouse 90+
```

#### STEP-2: DETERMINE HTML STRUCTURE

**Objective:** Plan the semantic structure

```
Cache Structure:
- Document type: HTML5
- Layout pattern: Standard web page
- Sections needed:
  ├─ Header with navigation
  ├─ Hero section
  ├─ Features section
  ├─ Pricing section
  ├─ Testimonials section
  ├─ CTA section
  ├─ Footer
```

**Stored in LOCAL_MEMORY.CACHE():**
```
HTML_STRUCTURE = {
  doctype: "html5",
  lang: "en",
  sections: [
    "header",
    "hero",
    "features",
    "pricing",
    "testimonials",
    "cta",
    "footer"
  ],
  semantic_tags: true,
  accessibility_level: "wcag2.1_aa",
  responsive: true
}
```

#### STEP-3: RETRIEVE & APPLY HTML RULES

**Objective:** Follow HTML best practices and standards

```
Retrieved from LOCAL_MEMORY.CACHE():

1. SEMANTIC RULES:
   ✓ Use <header>, <nav>, <main>, <section>, <article>, <aside>, <footer>
   ✓ Never use <div> when semantic tag exists
   ✓ Proper heading hierarchy (h1 > h2 > h3)

2. ACCESSIBILITY RULES:
   ✓ All images have alt text
   ✓ Forms have labels
   ✓ Color contrast minimum 4.5:1
   ✓ Keyboard navigation supported
   ✓ ARIA attributes where needed

3. METADATA RULES:
   ✓ charset="UTF-8" first in <head>
   ✓ viewport meta tag required
   ✓ descriptive <title> tag
   ✓ og:* tags for social sharing
   ✓ canonical URL

4. PERFORMANCE RULES:
   ✓ Critical CSS inlined
   ✓ Non-critical CSS deferred
   ✓ Scripts at end of body
   ✓ Images optimized and responsive
   ✓ Lazy loading for below-fold content

5. SECURITY RULES:
   ✓ No inline event handlers
   ✓ No dangerous HTML attributes
   ✓ Proper form validation
   ✓ CSRF protection
```

#### STEP-4: LIST REQUIREMENTS CHECKLIST

**Objective:** Create explicit requirements to track

```
REQUIREMENTS CHECKLIST:

SEMANTIC STRUCTURE:
☐ One <h1> per page
☐ Proper heading hierarchy
☐ Semantic sections identified
☐ Navigation marked with <nav>
☐ Main content in <main>
☐ Footer marked with <footer>

CONTENT STRUCTURE:
☐ Hero section with headline + CTA
☐ Features section with descriptions
☐ Pricing section with options
☐ Testimonials with attribution
☐ Contact/CTA section
☐ Footer with links + copyright

FORM ELEMENTS:
☐ All inputs have <label> elements
☐ Form validation attributes
☐ Submit button present
☐ Confirmation message

IMAGES & MEDIA:
☐ All images have descriptive alt text
☐ Responsive image implementation
☐ Image optimization
☐ Video captions if applicable

ACCESSIBILITY:
☐ Color contrast 4.5:1 minimum
☐ Focus indicators visible
☐ Keyboard navigation works
☐ Screen reader compatible
☐ ARIA labels where needed
☐ Language attribute on <html>

METADATA:
☐ <title> tag meaningful
☐ <meta description> present
☐ <meta viewport> configured
☐ Open Graph tags
☐ Canonical URL
☐ Favicon present

PERFORMANCE:
☐ CSS minified
☐ Images optimized
☐ Scripts deferred
☐ Critical CSS inlined
☐ Lighthouse score > 90

SECURITY:
☐ No inline JavaScript
☐ Form CSRF protection
☐ Input validation
☐ No dangerous attributes
```

#### STEP-5: CREATE GENERATION ROADMAP

**Objective:** Plan code generation like a route map

```
HTML GENERATION ROADMAP:

PHASE 1: FOUNDATION
├─ Generate <!DOCTYPE html>
├─ Create <html> with lang attribute
├─ Build <head> section
│  ├─ Meta charset
│  ├─ Viewport meta tag
│  ├─ Page title
│  ├─ Meta description
│  ├─ Favicon link
│  └─ CSS link
└─ Create <body> structure

PHASE 2: LAYOUT FRAMEWORK
├─ Add <header> with navigation
├─ Create main navigation <nav>
├─ Establish <main> container
├─ Create <section> elements for major areas
├─ Add <footer>
└─ Verify semantic structure

PHASE 3: CONTENT INSERTION
├─ Add hero section content
│  ├─ <h1> main headline
│  ├─ <p> subheading
│  └─ <button> or <a> for CTA
├─ Add features section
│  ├─ <h2> section heading
│  └─ Feature cards with descriptions
├─ Add pricing section
│  ├─ Pricing comparison table
│  └─ Option selectors
├─ Add testimonials
│  ├─ <blockquote> with attribution
│  └─ Author information
└─ Add footer links and copyright

PHASE 4: INTERACTIVITY
├─ Create contact form
│  ├─ <form> with action/method
│  ├─ Input fields with labels
│  ├─ Validation attributes
│  └─ Submit button
├─ Add interactive elements
│  ├─ Tabs or accordions
│  ├─ Modal dialogs
│  └─ Carousels
└─ Add data attributes for JavaScript

PHASE 5: ACCESSIBILITY
├─ Verify heading hierarchy
├─ Add alt text to all images
├─ Test color contrast
├─ Add ARIA attributes
│  ├─ aria-labels where needed
│  ├─ aria-expanded for toggle
│  └─ role attributes
├─ Test keyboard navigation
└─ Add skip link

PHASE 6: OPTIMIZATION
├─ Minify HTML
├─ Optimize images
├─ Defer non-critical CSS
├─ Move scripts to end
├─ Add performance meta tags
├─ Validate HTML
└─ Test in multiple browsers

ROADMAP: "Go to semantic structure phase, ensure all heading hierarchy, then add content sections step by step, integrate forms with accessibility, add ARIA attributes, optimize performance, validate against W3C standards, deploy to production."
```

#### STEP-6: EXECUTE GENERATION

**Objective:** Generate complete, production-ready HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Product Landing Page - Modern Software Solutions</title>
  <meta name="description" content="Discover our innovative software solution for modern businesses. Features, pricing, and customer testimonials.">
  <link rel="icon" href="/favicon.ico">
  <link rel="stylesheet" href="styles.css">
  <meta name="theme-color" content="#3498db">
  <meta property="og:title" content="Product Landing Page">
  <meta property="og:description" content="Modern software solutions for businesses">
  <meta property="og:image" content="https://example.com/og-image.jpg">
  <link rel="canonical" href="https://example.com">
</head>

<body>
  <!-- Skip Link -->
  <a href="#main" class="skip-link">Skip to main content</a>

  <!-- Header -->
  <header role="banner">
    <div class="logo">Company</div>
    <nav aria-label="Main navigation" role="navigation">
      <ul>
        <li><a href="#features">Features</a></li>
        <li><a href="#pricing">Pricing</a></li>
        <li><a href="#testimonials">Testimonials</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>
  </header>

  <!-- Main Content -->
  <main id="main" role="main">
    <!-- Hero Section -->
    <section class="hero" aria-labelledby="hero-heading">
      <h1 id="hero-heading">Modern Software Solution for Your Business</h1>
      <p>Build faster, scale bigger, succeed sooner with our platform.</p>
      <button class="cta-button" onclick="scrollToSection('contact')">
        Get Started Free
      </button>
    </section>

    <!-- Features Section -->
    <section id="features" aria-labelledby="features-heading">
      <h2 id="features-heading">Powerful Features</h2>
      <article class="feature-card">
        <h3>Real-time Collaboration</h3>
        <p>Work together seamlessly with your team in real-time.</p>
      </article>
      <article class="feature-card">
        <h3>Advanced Analytics</h3>
        <p>Make data-driven decisions with powerful insights.</p>
      </article>
      <article class="feature-card">
        <h3>Enterprise Security</h3>
        <p>Your data is protected with bank-grade security.</p>
      </article>
    </section>

    <!-- Pricing Section -->
    <section id="pricing" aria-labelledby="pricing-heading">
      <h2 id="pricing-heading">Simple, Transparent Pricing</h2>
      <table>
        <thead>
          <tr>
            <th scope="col">Plan</th>
            <th scope="col">Users</th>
            <th scope="col">Price</th>
            <th scope="col">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <th scope="row">Starter</th>
            <td>1-5</td>
            <td>$29/month</td>
            <td><button>Choose</button></td>
          </tr>
          <tr>
            <th scope="row">Professional</th>
            <td>5-50</td>
            <td>$99/month</td>
            <td><button>Choose</button></td>
          </tr>
          <tr>
            <th scope="row">Enterprise</th>
            <td>Unlimited</td>
            <td>Custom</td>
            <td><button>Contact</button></td>
          </tr>
        </tbody>
      </table>
    </section>

    <!-- Testimonials Section -->
    <section id="testimonials" aria-labelledby="testimonials-heading">
      <h2 id="testimonials-heading">What Our Customers Say</h2>
      <blockquote>
        <p>"This platform transformed how our team works. Highly recommended!"</p>
        <footer>— Sarah Johnson, CTO at TechCorp</footer>
      </blockquote>
      <blockquote>
        <p>"Best investment we made for our business. ROI within 3 months."</p>
        <footer>— Mike Chen, Founder at StartupXYZ</footer>
      </blockquote>
    </section>

    <!-- Contact/CTA Section -->
    <section id="contact" aria-labelledby="contact-heading">
      <h2 id="contact-heading">Ready to Get Started?</h2>
      <form action="/submit" method="POST" novalidate>
        <div class="form-group">
          <label for="name">Full Name:</label>
          <input type="text" id="name" name="name" required aria-describedby="name-hint">
          <span id="name-hint">Your full name</span>
        </div>

        <div class="form-group">
          <label for="email">Email Address:</label>
          <input type="email" id="email" name="email" required aria-describedby="email-hint">
          <span id="email-hint">We'll never share your email</span>
        </div>

        <div class="form-group">
          <label for="company">Company:</label>
          <input type="text" id="company" name="company" required>
        </div>

        <div class="form-group">
          <label for="message">Message:</label>
          <textarea id="message" name="message" rows="5" required></textarea>
        </div>

        <button type="submit" class="submit-button">Send Message</button>
      </form>
    </section>
  </main>

  <!-- Footer -->
  <footer role="contentinfo">
    <div class="footer-content">
      <nav aria-label="Footer navigation">
        <ul>
          <li><a href="/about">About</a></li>
          <li><a href="/privacy">Privacy</a></li>
          <li><a href="/terms">Terms</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
      <p>&copy; 2025 Company. All rights reserved.</p>
    </div>
  </footer>

  <!-- Scripts at end -->
  <script src="script.js"></script>
</body>
</html>
```

---

## BEST PRACTICES & STANDARDS

### HTML Writing Standards

#### 1. **Use Semantic HTML**

```html
❌ BAD:
<div class="header">
  <div class="title">Welcome</div>
  <div class="nav">
    <div class="link"><a href="/">Home</a></div>
  </div>
</div>

✅ GOOD:
<header>
  <h1>Welcome</h1>
  <nav>
    <a href="/">Home</a>
  </nav>
</header>
```

#### 2. **Maintain Proper Heading Hierarchy**

```html
❌ BAD:
<h1>Page Title</h1>
<h3>Section</h3>  <!-- Skipped h2 -->
<h2>Subsection</h2>  <!-- Out of order -->

✅ GOOD:
<h1>Page Title</h1>
<h2>Section</h2>
<h3>Subsection</h3>
<h3>Another Subsection</h3>
<h2>Another Section</h2>
```

#### 3. **Always Use Labels for Form Inputs**

```html
❌ BAD:
<input type="text" placeholder="Enter name">

✅ GOOD:
<label for="name">Name:</label>
<input type="text" id="name" name="name" placeholder="Enter your name">
```

#### 4. **Provide Descriptive Alt Text**

```html
❌ BAD:
<img src="photo.jpg" alt="image">
<img src="chart.png" alt="">

✅ GOOD:
<img src="sunset.jpg" alt="Sunset over the Pacific Ocean">
<img src="sales-chart.png" alt="Q4 sales by region, showing 23% growth">
```

#### 5. **Use Responsive Images**

```html
❌ BAD:
<img src="image.jpg">

✅ GOOD:
<picture>
  <source media="(min-width: 1200px)" srcset="image-large.jpg">
  <source media="(min-width: 600px)" srcset="image-medium.jpg">
  <img src="image-small.jpg" alt="Description">
</picture>
```

#### 6. **Validate HTML Regularly**

```bash
# Use W3C Validator
https://validator.w3.org/

# Or validate locally
npm install -g html-validate
html-validate index.html
```

#### 7. **Test Accessibility**

```bash
# Use accessibility testing tools
- WAVE (Web Accessibility Evaluation Tool)
- axe DevTools
- NVDA Screen Reader
- Lighthouse Accessibility Audit
```

#### 8. **Optimize Performance**

```html
<!-- Critical CSS inline -->
<style>
  body { font-family: sans-serif; }
</style>

<!-- Non-critical CSS deferred -->
<link rel="stylesheet" href="non-critical.css" media="print" onload="this.media='all'">

<!-- Images optimized and responsive -->
<picture>
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="Description">
</picture>

<!-- Scripts deferred or async -->
<script src="script.js" defer></script>
```

---

## SAFETY & VALIDATION RULES

### HTML Security

#### 1. **Prevent XSS (Cross-Site Scripting)**

```html
❌ DANGEROUS:
<div innerHTML="<script>alert('XSS')</script>"></div>

✅ SAFE:
<div>Text content only</div>
<!-- Use textContent in JavaScript, not innerHTML -->
```

#### 2. **Avoid Dangerous Attributes**

```html
❌ NEVER USE:
<img src="x" onerror="alert('XSS')">
<a href="javascript:alert('XSS')">Click</a>
<div onmouseover="maliciousCode()">

✅ USE:
<img src="image.jpg" alt="Description">
<a href="/page">Link</a>
<!-- Use event listeners in JavaScript files -->
```

#### 3. **Form Security**

```html
❌ BAD:
<form action="/process" method="GET">
  <input type="password" name="password">
</form>

✅ GOOD:
<form action="/process" method="POST">
  <input type="hidden" name="csrf_token" value="...">
  <input type="password" name="password">
</form>
```

#### 4. **Content Security Policy**

```html
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'">
```

### HTML Validation Rules

#### Complete Validation Checklist

```
STRUCTURE VALIDATION:
☐ <!DOCTYPE html> present and first
☐ <html> element wraps all content
☐ <head> and <body> properly closed
☐ All tags properly nested
☐ No missing closing tags
☐ lang attribute on <html>

METADATA VALIDATION:
☐ charset="UTF-8" specified
☐ <title> present and unique
☐ <meta name="viewport"> present
☐ <meta name="description"> present

SEMANTIC VALIDATION:
☐ Proper heading hierarchy
☐ One <main> per page
☐ <nav> only for navigation
☐ <section>, <article> properly used
☐ No <h2-h6> without <h1>

ACCESSIBILITY VALIDATION:
☐ All images have alt text
☐ All form inputs have labels
☐ Color contrast minimum 4.5:1
☐ Focus indicators visible
☐ ARIA roles used correctly
☐ Link text descriptive

PERFORMANCE VALIDATION:
☐ Images optimized
☐ Critical CSS inlined
☐ Scripts at end of body
☐ No render-blocking resources
☐ Responsive design working
☐ Lighthouse score > 90

SECURITY VALIDATION:
☐ No inline JavaScript
☐ No dangerous attributes
☐ Form CSRF protection present
☐ Input validation present
☐ No hardcoded secrets

CODE QUALITY VALIDATION:
☐ Consistent indentation
☐ Proper whitespace
☐ Comments where needed
☐ No dead code
☐ Valid W3C HTML
```

---

## VERSION MANAGEMENT

### HTML Version System

```
VERSION NAMING:
v1.0.0 - Initial release
v1.1.0 - Added features (backward compatible)
v1.1.1 - Bug fixes
v2.0.0 - Breaking changes

CHANGELOG FORMAT:
v1.2.0 - Added responsive images
  ├─ Added srcset and sizes attributes
  ├─ Added picture element
  └─ Updated accessibility labels

v1.1.5 - Fixed form validation
  ├─ Added required attributes
  ├─ Fixed input patterns
  └─ Updated error messages

v1.1.4 - Improved performance
  ├─ Inlined critical CSS
  ├─ Deferred non-critical resources
  └─ Optimized images
```

---

## CONCLUSION

HTML is the foundation of all web content. When written with semantic structure, accessibility considerations, and best practices, it creates web experiences that are:

- ✅ **Accessible** to all users
- ✅ **Performant** across devices
- ✅ **Maintainable** for teams
- ✅ **SEO-friendly** for discovery
- ✅ **Secure** against attacks
- ✅ **Future-proof** as standards evolve

### Key Takeaways

1. **Use semantic HTML** - Tags should mean something
2. **Accessibility first** - Build for all users
3. **Progressive enhancement** - Base functionality without JavaScript
4. **Mobile-first approach** - Design for smallest screen first
5. **Validate regularly** - Use W3C Validator
6. **Test thoroughly** - Accessibility + Performance + Security
7. **Maintain versions** - Track changes with clear documentation
8. **Follow standards** - W3C HTML Living Standard
9. **Optimize performance** - Keep users happy
10. **Security always** - Protect user data

---

