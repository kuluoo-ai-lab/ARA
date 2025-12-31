# CSS LANGUAGE FORMAL SPECIFICATION
## Cascading Style Sheets - Complete Code Generation Standard

---

## EXECUTIVE SUMMARY

**CSS (Cascading Style Sheets)** is a declarative, property-based styling language designed to control the visual presentation of HTML documents with responsive design, accessibility, and performance built-in.

### Language Goals

- ✅ **Visual Control:** Separate presentation from structure
- ✅ **Responsiveness:** Mobile-first, device-agnostic styling
- ✅ **Accessibility:** WCAG color contrast and readability
- ✅ **Performance:** Optimized stylesheets and critical CSS
- ✅ **Maintainability:** DRY principles with variables and mixins
- ✅ **Browser Support:** 99%+ compatibility across modern browsers
- ✅ **Animation:** Smooth transitions and keyframe animations
- ✅ **Flexibility:** Flexbox, Grid, and modern layout systems

---

## 12 PRIMARY CSS KEYWORDS

### 1. **SELECTOR** - Element Selection & Targeting

**Purpose:** Target specific HTML elements for styling

**Keywords:**
- `element` - Element selector
- `.class` - Class selector
- `#id` - ID selector
- `[attribute]` - Attribute selector
- `selector:pseudo-class` - Pseudo-class selector
- `selector::pseudo-element` - Pseudo-element selector
- `selector + selector` - Adjacent sibling
- `selector > selector` - Child selector
- `selector selector` - Descendant selector
- `selector ~ selector` - General sibling

**Syntax:**
```css
/* Element selector */
p { color: black; }

/* Class selector */
.button { padding: 10px; }

/* ID selector */
#header { background: blue; }

/* Attribute selector */
input[type="text"] { border: 1px solid gray; }

/* Pseudo-class */
a:hover { color: red; }

/* Pseudo-element */
p::first-line { font-weight: bold; }

/* Combinators */
div > p { margin: 0; }              /* Child */
div p { color: gray; }              /* Descendant */
h1 + p { margin-top: 0; }          /* Adjacent sibling */
h1 ~ p { line-height: 1.5; }       /* General sibling */

/* Multiple selectors */
h1, h2, h3 { font-family: Arial; }
```

**Best Practices:**
- Prefer classes over IDs
- Use specific selectors (avoid universal `*`)
- Keep specificity low for maintainability
- Use semantic class names
- Avoid deep nesting (max 3-4 levels)

---

### 2. **BOX** - Box Model & Spacing

**Purpose:** Control element dimensions and spacing

**Keywords:**
- `width` - Element width
- `height` - Element height
- `padding` - Internal spacing
- `margin` - External spacing
- `border` - Element border
- `box-sizing` - Box sizing model
- `display` - Display type
- `overflow` - Overflow behavior

**Syntax:**
```css
/* Box dimensions */
.container {
  width: 100%;
  height: auto;
  max-width: 1200px;
  min-height: 100vh;
}

/* Padding (internal spacing) */
.box {
  padding: 20px;                    /* All sides */
  padding: 10px 20px;              /* Vertical, Horizontal */
  padding: 10px 20px 15px 5px;    /* Top, Right, Bottom, Left */
}

/* Margin (external spacing) */
.element {
  margin: 0 auto;                   /* Center horizontally */
  margin-top: 20px;
  margin-bottom: 30px;
}

/* Border */
.bordered {
  border: 1px solid #ccc;
  border-radius: 8px;
}

/* Box sizing */
* {
  box-sizing: border-box;           /* Include padding/border in width */
}

/* Display */
.flex { display: flex; }
.grid { display: grid; }
.inline { display: inline-block; }
.block { display: block; }
.none { display: none; }
```

**Rules:**
- Always use `box-sizing: border-box`
- Use margin for spacing between elements
- Use padding for internal element spacing
- Remember margin collapsing
- Use shorthand for efficiency

---

### 3. **LAYOUT** - Flexbox & Grid Systems

**Purpose:** Create responsive, flexible layouts

**Keywords:**
- `display: flex` - Flexbox container
- `flex-direction` - Flex direction
- `justify-content` - Horizontal alignment
- `align-items` - Vertical alignment
- `display: grid` - Grid container
- `grid-template-columns` - Grid columns
- `grid-template-rows` - Grid rows
- `gap` - Spacing between items

**Syntax:**
```css
/* Flexbox */
.flex-container {
  display: flex;
  flex-direction: row;              /* row, column, row-reverse, column-reverse */
  justify-content: space-between;   /* Horizontal alignment */
  align-items: center;              /* Vertical alignment */
  gap: 20px;                        /* Space between items */
  flex-wrap: wrap;                  /* Wrap items to next line */
}

.flex-item {
  flex: 1;                          /* Grow equally */
  flex-basis: 200px;               /* Base size */
}

/* CSS Grid */
.grid-container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  grid-template-rows: auto 1fr auto;
  gap: 20px;
}

.grid-item:nth-child(1) {
  grid-column: 1 / 3;              /* Span 2 columns */
  grid-row: 1;
}

/* Responsive Grid */
@media (max-width: 768px) {
  .grid-container {
    grid-template-columns: 1fr;    /* Single column on mobile */
  }
}
```

**Best Practices:**
- Use Flexbox for 1D layouts
- Use Grid for 2D layouts
- Use `gap` instead of margins
- Always plan responsive breakpoints
- Test on multiple devices

---

### 4. **COLOR** - Colors & Gradients

**Purpose:** Define colors and color schemes

**Keywords:**
- `color` - Text color
- `background-color` - Background color
- `background-image` - Background image/gradient
- `opacity` - Element opacity
- `rgba()` - Color with alpha
- `linear-gradient()` - Linear gradient
- `radial-gradient()` - Radial gradient

**Syntax:**
```css
/* Text color */
.text { color: #333; }

/* Background colors */
.bg-primary { background-color: #3498db; }
.bg-secondary { background-color: #2ecc71; }

/* Opacity */
.transparent { opacity: 0.5; }
.semi-transparent { color: rgba(0, 0, 0, 0.8); }

/* Linear gradient */
.gradient-h {
  background: linear-gradient(to right, #ff0000, #0000ff);
}

/* Radial gradient */
.gradient-radial {
  background: radial-gradient(circle, #ff0000, #0000ff);
}

/* Color variables */
:root {
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --text-color: #333;
  --bg-color: #fff;
  --border-color: #ddd;
}

.button {
  background-color: var(--primary-color);
  color: white;
}
```

**Accessibility Rules:**
- Contrast ratio minimum 4.5:1 for normal text
- Contrast ratio minimum 3:1 for large text
- Don't use color alone to convey information
- Use semantic color names

---

### 5. **TYPOGRAPHY** - Fonts & Text Styling

**Purpose:** Control text appearance and readability

**Keywords:**
- `font-family` - Font selection
- `font-size` - Text size
- `font-weight` - Font weight
- `font-style` - Font style (italic, normal)
- `line-height` - Line height
- `letter-spacing` - Letter spacing
- `text-align` - Text alignment
- `text-decoration` - Text decoration

**Syntax:**
```css
/* Font selection */
body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 
               Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  line-height: 1.5;
  color: #333;
}

/* Font weight */
.bold { font-weight: 700; }
.semibold { font-weight: 600; }
.normal { font-weight: 400; }

/* Text styling */
.italic { font-style: italic; }
.underline { text-decoration: underline; }
.uppercase { text-transform: uppercase; }
.capitalize { text-transform: capitalize; }

/* Text alignment */
.center { text-align: center; }
.justify { text-align: justify; }
.left { text-align: left; }
.right { text-align: right; }

/* Web fonts */
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

.heading {
  font-family: 'Roboto', sans-serif;
  font-size: 32px;
  font-weight: 700;
  line-height: 1.2;
}

.body {
  font-family: 'Roboto', sans-serif;
  font-size: 16px;
  line-height: 1.6;
}
```

**Best Practices:**
- Use system fonts or web-safe fonts
- Limit font weights (typically 400, 600, 700)
- Use `line-height: 1.5+` for readability
- Use `letter-spacing` sparingly
- Test on multiple devices and browsers

---

### 6. **POSITIONING** - Position & Stacking

**Purpose:** Control element positioning

**Keywords:**
- `position` - Positioning type
- `top`, `right`, `bottom`, `left` - Position offsets
- `z-index` - Stacking order
- `float` - Float positioning (legacy)
- `sticky` - Sticky positioning

**Syntax:**
```css
/* Static positioning (default) */
.static { position: static; }

/* Relative positioning */
.relative {
  position: relative;
  top: 10px;
  left: 20px;
}

/* Absolute positioning */
.absolute {
  position: absolute;
  top: 0;
  right: 0;
  width: 100px;
}

/* Fixed positioning */
.fixed {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
}

/* Sticky positioning */
.sticky {
  position: sticky;
  top: 0;
  background: white;
}

/* Z-index (stacking) */
.modal { z-index: 1000; }
.tooltip { z-index: 1001; }
.notification { z-index: 1002; }
```

**Rules:**
- Use `position: relative` for relative positioning
- Absolute/fixed require positioned parent
- Use `z-index` with restraint
- Avoid float (use Flexbox/Grid instead)
- Create stacking context hierarchy

---

### 7. **RESPONSIVE** - Media Queries & Breakpoints

**Purpose:** Create device-responsive designs

**Keywords:**
- `@media` - Media query
- `(max-width)` - Maximum width breakpoint
- `(min-width)` - Minimum width breakpoint
- `(orientation)` - Device orientation
- `(prefers-color-scheme)` - Color scheme preference

**Syntax:**
```css
/* Mobile-first approach */
.container {
  width: 100%;
  padding: 10px;
}

/* Tablet (768px and up) */
@media (min-width: 768px) {
  .container {
    width: 90%;
    padding: 20px;
  }
  
  .column {
    flex: 0 0 calc(50% - 10px);
  }
}

/* Desktop (1024px and up) */
@media (min-width: 1024px) {
  .container {
    width: 1000px;
    margin: 0 auto;
  }
  
  .column {
    flex: 0 0 calc(33.333% - 10px);
  }
}

/* Large desktop (1440px and up) */
@media (min-width: 1440px) {
  .container {
    width: 1400px;
  }
}

/* Dark mode preference */
@media (prefers-color-scheme: dark) {
  body {
    background: #1a1a1a;
    color: #fff;
  }
}

/* Print styles */
@media print {
  body { background: white; }
  .no-print { display: none; }
}
```

**Standard Breakpoints:**
```css
/* Mobile: 0-767px */
/* Tablet: 768px-1023px */
/* Desktop: 1024px-1439px */
/* Large: 1440px+ */
```

---

### 8. **TRANSFORM** - Transforms & Animations

**Purpose:** Create animations and visual effects

**Keywords:**
- `transform` - CSS transformations
- `transition` - Smooth transitions
- `animation` - Keyframe animations
- `@keyframes` - Define animations
- `translate`, `rotate`, `scale` - Transform functions

**Syntax:**
```css
/* Basic transforms */
.scale:hover {
  transform: scale(1.1);
}

.rotate {
  transform: rotate(45deg);
}

.translate {
  transform: translateX(10px) translateY(20px);
}

/* Combined transforms */
.complex {
  transform: translate(50%, -50%) rotate(45deg) scale(1.2);
}

/* Transitions */
.button {
  background-color: blue;
  transition: background-color 0.3s ease;
}

.button:hover {
  background-color: darkblue;
}

/* Keyframe animations */
@keyframes slideIn {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.animated-element {
  animation: slideIn 0.5s ease forwards;
}

/* Multiple animations */
@keyframes rotate360 {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.spinner {
  animation: rotate360 2s linear infinite;
}
```

**Performance Tips:**
- Use `transform` and `opacity` for smooth animations
- Avoid animating `width`, `height`, `top`, `left`
- Use `will-change` for performance hints
- Keep animations under 300-500ms for UI feedback

---

### 9. **SHADOW** - Shadows & Effects

**Purpose:** Add depth with shadows and effects

**Keywords:**
- `box-shadow` - Element shadow
- `text-shadow` - Text shadow
- `filter` - Visual effects
- `blur`, `brightness`, `contrast` - Filter functions

**Syntax:**
```css
/* Box shadow */
.card {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.card:hover {
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

/* Multiple shadows */
.depth {
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12),
              0 1px 2px rgba(0, 0, 0, 0.24);
}

/* Text shadow */
.text-shadow {
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

/* Filters */
.blur { filter: blur(5px); }
.brightness { filter: brightness(1.2); }
.contrast { filter: contrast(1.5); }
.grayscale { filter: grayscale(100%); }
.opacity { filter: opacity(0.5); }
.saturate { filter: saturate(2); }
.sepia { filter: sepia(100%); }
```

---

### 10. **BORDER** - Borders & Outlines

**Purpose:** Create borders and define element boundaries

**Keywords:**
- `border` - Element border
- `border-radius` - Rounded corners
- `outline` - Focus outline
- `border-style` - Border style

**Syntax:**
```css
/* Basic border */
.border {
  border: 1px solid #ddd;
}

/* Bordered sides */
.border-top {
  border-top: 2px solid blue;
}

.border-bottom {
  border-bottom: 3px dashed red;
}

/* Border radius */
.rounded {
  border-radius: 8px;
}

.pill {
  border-radius: 50px;
}

.circle {
  border-radius: 50%;
}

/* Border styles */
.solid { border: 1px solid gray; }
.dashed { border: 1px dashed gray; }
.dotted { border: 1px dotted gray; }
.double { border: 3px double gray; }

/* Outline (focus indicator) */
.button:focus {
  outline: 2px solid blue;
  outline-offset: 2px;
}
```

---

### 11. **BACKGROUND** - Background Properties

**Purpose:** Control background appearance

**Keywords:**
- `background-color` - Background color
- `background-image` - Background image
- `background-size` - Background size
- `background-position` - Background position
- `background-attachment` - Background attachment

**Syntax:**
```css
/* Simple background */
.bg {
  background-color: #f0f0f0;
}

/* Background image */
.hero {
  background-image: url('hero.jpg');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}

/* Gradient background */
.gradient {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

/* Multiple backgrounds */
.complex {
  background-image: 
    linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url('hero.jpg');
  background-size: cover;
  background-position: center;
}

/* Responsive background */
@media (max-width: 768px) {
  .hero {
    background-attachment: scroll;  /* Fixed doesn't work well on mobile */
  }
}
```

---

### 12. **OVERFLOW** - Overflow & Scrolling

**Purpose:** Control content overflow behavior

**Keywords:**
- `overflow` - Overflow behavior
- `overflow-x` - Horizontal overflow
- `overflow-y` - Vertical overflow
- `text-overflow` - Text overflow

**Syntax:**
```css
/* Visible (default) */
.overflow-visible {
  overflow: visible;
}

/* Hidden */
.overflow-hidden {
  overflow: hidden;
}

/* Scroll */
.overflow-scroll {
  overflow: scroll;
  height: 200px;
}

/* Auto */
.overflow-auto {
  overflow: auto;
  height: 300px;
}

/* Separate overflow directions */
.overflow-xy {
  overflow-x: auto;
  overflow-y: hidden;
}

/* Text overflow */
.text-truncate {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/* Multi-line truncate */
.text-clamp {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

---

## 6-STEP CSS GENERATION WORKFLOW

### STEP-1: UNDERSTAND DESIGN INTENT

```
Questions:
✓ What is the visual style? (modern, minimalist, colorful)
✓ What are the brand colors?
✓ What typography is needed?
✓ What device breakpoints required?
✓ Any animations/interactions?
✓ Accessibility requirements?
```

### STEP-2: DEFINE CSS ARCHITECTURE

```
CSS Structure:
- Variables (colors, fonts, spacing)
- Reset/Normalize
- Typography
- Layout (Flexbox/Grid)
- Components
- Utilities
- Responsive styles
- Animations
```

### STEP-3: RETRIEVE CSS RULES

```
From LOCAL_MEMORY.CACHE():
1. SEMANTIC CLASSNAMES (BEM, SMACSS)
2. MOBILE-FIRST APPROACH
3. DRY PRINCIPLES (Variables, Mixins)
4. ACCESSIBILITY STANDARDS
5. PERFORMANCE OPTIMIZATION
6. BROWSER COMPATIBILITY
```

### STEP-4: REQUIREMENTS CHECKLIST

```
☐ Color palette defined
☐ Typography system set
☐ Spacing system consistent
☐ Responsive breakpoints identified
☐ Animation specs listed
☐ Accessibility contrast verified
☐ Performance budget set
```

### STEP-5: GENERATION ROADMAP

```
PHASE 1: FOUNDATION
├─ CSS Reset/Normalize
├─ CSS Variables
├─ Typography setup
└─ Color system

PHASE 2: LAYOUT
├─ Grid system
├─ Flexbox patterns
└─ Responsive design

PHASE 3: COMPONENTS
├─ Button styles
├─ Card patterns
├─ Form elements
└─ Navigation

PHASE 4: POLISH
├─ Animations
├─ Shadows
├─ Hover states
└─ Focus indicators

PHASE 5: RESPONSIVE
├─ Mobile styles
├─ Tablet adjustments
└─ Desktop refinement

PHASE 6: OPTIMIZATION
├─ Minification
├─ Critical CSS
├─ Tree-shaking
└─ Performance testing
```

### STEP-6: EXECUTE GENERATION

```css
/* Production-ready CSS structure */

/* 1. VARIABLES */
:root {
  /* Colors */
  --primary: #3498db;
  --secondary: #2ecc71;
  --danger: #e74c3c;
  --text: #333;
  --bg: #fff;
  --border: #ddd;
  
  /* Typography */
  --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto;
  --font-size: 16px;
  --line-height: 1.5;
  
  /* Spacing */
  --spacing-unit: 8px;
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
  --spacing-xl: 32px;
  
  /* Shadows */
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.1);
  --shadow-md: 0 4px 6px rgba(0,0,0,0.1);
  --shadow-lg: 0 10px 15px rgba(0,0,0,0.2);
  
  /* Breakpoints */
  --mobile: 0;
  --tablet: 768px;
  --desktop: 1024px;
  --large: 1440px;
}

/* 2. RESET */
* { margin: 0; padding: 0; box-sizing: border-box; }
body { font-family: var(--font-family); color: var(--text); }
a { color: inherit; text-decoration: none; }

/* 3. TYPOGRAPHY */
h1 { font-size: 32px; font-weight: 700; }
h2 { font-size: 24px; font-weight: 700; }
p { line-height: var(--line-height); }

/* 4. LAYOUT */
.container { max-width: 1200px; margin: 0 auto; padding: 0 var(--spacing-md); }
.grid { display: grid; gap: var(--spacing-md); }
.flex { display: flex; gap: var(--spacing-md); }

/* 5. COMPONENTS */
.button {
  padding: var(--spacing-sm) var(--spacing-md);
  background: var(--primary);
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background 0.3s ease;
}

.button:hover { background: darken(var(--primary), 10%); }

/* 6. RESPONSIVE */
@media (min-width: 768px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 1024px) {
  .grid { grid-template-columns: repeat(3, 1fr); }
}
```

---

## BEST PRACTICES

1. **Use CSS Variables** for consistent theming
2. **Mobile-First Approach** - Start small, add complexity
3. **Semantic Class Names** - Use BEM or SMACSS
4. **Avoid Deep Nesting** - Keep specificity low
5. **Performance First** - Optimize critical CSS
6. **Accessibility Always** - WCAG contrast ratios
7. **Test Responsiveness** - Multiple devices
8. **Keep DRY** - Don't Repeat Yourself
9. **Document Colors** - Use semantic names
10. **Validate CSS** - Use W3C Validator

---

