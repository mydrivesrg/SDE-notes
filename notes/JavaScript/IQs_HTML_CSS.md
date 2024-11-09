## HTML5:
## 1. Selectors in HTML
- Element selector
- ID selector
- class selector
- Attribute selector
- Universal selector
- Child Selector
- Pseudo Selector
 - :hover, :active, :focus, :first-child, :last-child, nth-child(n)
---------------------------------
## 2. innerHTML
- `innerHTML` is a property in Javascript that allows you to get or set the HTML content within an element.
#### Get HTML content:
```java
var element = document.getElementById('myElement');
var htmlContent = element.innerHtml;
console.log(htmlContent):
```
#### set HTML content:
```java
var element = document.getElementById('myElement');
element.innerHtml = <p>This is a new paragrapj </p>;
```
---------------------------------
## Web accessibility?**
- Web accessibility refers to the inclusive practice of ensuring that website, web applications, and web content are usable and accessible to all people, ragardless of their physical or cognitive abilities, disabilities, or the devices they use to access the web.
- 
---------------------------------
## 4. **Progressive Web App*
- PWAs provide an app-like experience to users, including features like smooth transitions, immersive full-screen mode, and the ability to add shortcuts to the home screen.
- PWAs can work offline or in areas with poor connectivity by caching resources and content locally. This allows users to continue using the app even when they are offline or experiencing network issues.
---------------------------------
## 5. **Service Worker in PWA**
- A Service Worker is a key component of Progressive Web Apps (PWAs) that enables features like offline functionality, push notifications, and background sync.
- It is a JavaScript file that runs separately from the main browser thread and can intercept network
requests, cache resources, and perform background tasks.
-------------------------------------------
## 6. **How to make website lightweight?**
To make a website lightweight:

1. **Optimize Images**: Compress and resize images to reduce their file size without sacrificing quality. Use modern image formats like WebP and lazy loading techniques to load images only when they're needed.

2. **Minimize HTTP Requests**: Reduce the number of HTTP requests by combining CSS and JavaScript files, using CSS sprites for icons, and limiting the use of external resources like fonts and scripts.

3. **Enable Caching**: Leverage browser caching by setting appropriate cache headers for static assets and resources. This allows the browser to store files locally, reducing the need to download them on subsequent visits.

4. **Optimize Code**: Minify and concatenate CSS and JavaScript files to remove unnecessary whitespace and comments. Optimize code structure and eliminate redundant or unused code to improve loading times and overall performance.
_________________________________________________________________________
## CSS3:

## 1. **What is CSS?**
- CSS stands fr cascading Style Sheets.
- It's style sheet language used to style the HTML elements and pages.
- It defines how the page should be rendered on screen.


## 2. **Position Attribute in CSS**

The `position` attribute in CSS is used to specify the positioning behavior of an element within its containing element. It allows you to control the layout and positioning of elements on a web page.

There are several values for the `position` attribute:

1. **Static**:
   - Default value. Elements are positioned according to the normal flow of the document. This means that elements are displayed in the order they appear in the HTML code.

2. **Relative**:
   - Elements are positioned relative to their normal position in the document flow. Using `top`, `right`, `bottom`, and `left` properties, you can shift the element from its normal position without affecting the layout of other elements.

3. **Absolute**:
   - Elements are removed from the normal document flow and positioned relative to the nearest positioned ancestor. If no ancestor is positioned, it's positioned relative to the initial containing block (usually the `<html>` element).

4. **Fixed**:
   - Elements are removed from the normal document flow and positioned relative to the viewport (the browser window). They remain fixed in their position even when the page is scrolled.

5. **Sticky**:
   - Elements are positioned based on the user's scroll position. It acts like `relative` positioning until an element reaches a specified point, then it "sticks" to that position as the user scrolls.

Each `position` value has its own behavior and use cases, allowing you to create complex layouts and designs in your web pages.

## 3. **FlexBox**
## 4. Grid:
-----------------------------------
## 5. **Display:none vs visibility:hiddeb**
Both `display: none;` and `visibility: hidden;` are CSS properties used to hide elements on a webpage, but they achieve this in slightly different ways:

1. **display: none;**:
   - This property removes the element from the document flow entirely. It's as if the element doesn't exist in the HTML structure.
   - The element will not take up any space on the webpage.
   - Other elements will act as if the hidden element isn't there at all.

   ```css
   .hidden {
       display: none;
   }
   ```

2. **visibility: hidden;**:
   - This property hides the element while still preserving its space in the layout.
   - The element is not visible, but it still occupies space and affects the layout of other elements around it.
   - Event handlers and scripts can still interact with the element, as it's still part of the DOM.

   ```css
   .hidden {
       visibility: hidden;
   }
   ```
--------------------------------------
1. **What is the purpose of the `<!DOCTYPE html>` declaration in HTML5?**
   - **Answer:** The `<!DOCTYPE html>` declaration defines the document type and ensures that the browser renders the page in standards mode.

2. **Explain the new semantic elements introduced in HTML5 and their purpose.**
   - **Answer:** HTML5 introduced semantic elements like `<header>`, `<footer>`, `<nav>`, `<section>`, `<article>`, `<aside>`, and `<main>`. They provide a clearer structure to web pages, making it easier for search engines and developers to understand the content's meaning.

3. **What is the difference between `<script async>` and `<script defer>`?**
   - **Answer:** 
     - `<script async>` loads and executes the script asynchronously, allowing the HTML parsing to continue without waiting for the script to finish loading.
     - `<script defer>` defers the script execution until the HTML parsing is complete, ensuring the script is executed in order.

   ```html
   <!-- Example with async -->
   <script src="script.js" async></script>

   <!-- Example with defer -->
   <script src="script.js" defer></script>
   ```

4. **Explain the `srcset` attribute in HTML5 for responsive images.**
   - **Answer:** The `srcset` attribute allows specifying multiple image sources with different resolutions or sizes. It helps the browser to choose the appropriate image based on the device's pixel density or viewport size.

   ```html
   <img src="image.jpg" srcset="image.jpg 1x, image@2x.jpg 2x" alt="Responsive Image">
   ```

5. **What is the purpose of the `localStorage` and `sessionStorage` objects in HTML5?**
   - **Answer:** 
     - `localStorage` stores data with no expiration date, allowing the data to persist even after the browser is closed.
     - `sessionStorage` stores data for one session only, clearing the data when the browser is closed.

   ```javascript
   // Storing data in localStorage
   localStorage.setItem('key', 'value');

   // Retrieving data from localStorage
   const data = localStorage.getItem('key');
   ```

6. **Explain the `rem` unit in CSS3 and how it differs from `em`.**
   - **Answer:** The `rem` unit represents the font size of the root element (`html`), while `em` represents the font size of the current element. `rem` is more predictable and easier to manage in complex layouts compared to `em`.

   ```css
   body {
     font-size: 16px; /* 1rem = 16px */
   }

   .box {
     font-size: 1.5rem; /* 1.5rem = 24px */
     padding: 1em; /* 1em = 24px (if parent's font-size is 16px) */
   }
   ```

7. **How can you achieve a sticky header in CSS?**
   - **Answer:** Use the `position: sticky;` property on the header element along with `top: 0;` to make it stick to the top of the viewport when scrolling.

   ```css
   header {
     position: sticky;
     top: 0;
     background-color: #fff;
     /* Other styles */
   }
   ```

8. **Explain the `currentColor` keyword in CSS and where it can be used.**
   - **Answer:** The `currentColor` keyword represents the value of the element's `color` property. It can be used to inherit the current text color for other properties like borders or backgrounds.

   ```css
   .box {
     color: red;
     border: 2px solid currentColor; /* Border color will be red */
     /* Other styles */
   }
   ```

9. **What are CSS variables (custom properties) and how do you define and use them?**
   - **Answer:** CSS variables allow storing reusable values in CSS. They are defined using the `--variable-name` syntax and accessed using the `var()` function.

   ```css
   :root {
     --primary-color: #007bff;
   }

   .button {
     background-color: var(--primary-color);
     /* Other styles */
   }
   ```

10. **Explain the difference between `flexbox` and `grid` layout in CSS3.**
    - **Answer:** 
      - Flexbox is a one-dimensional layout model used for arranging items in a row or column.
      - Grid is a two-dimensional layout model used for creating grid-based layouts with rows and columns.

11. **What is the `::before` and `::after` pseudo-elements in CSS3 used for? Provide examples.**
    - **Answer:** `::before` and `::after` pseudo-elements are used to insert content before and after an element's content, respectively.

    ```css
    .box::before {
      content: 'Before';
    }

    .box::after {
      content: 'After';
    }
    ```

12. **Explain the concept of CSS inheritance and how it works.**
    - **Answer:** CSS inheritance is the process where styles are applied to an element based on its parent-child relationship. Children inherit styles from their parent unless overridden.

13. **What are media queries in CSS3 and how do you use them for responsive design?**
    - **Answer:** Media queries allow applying different styles based on the device's characteristics such as screen width, height, orientation, etc., enabling responsive design.

    ```css
    @media screen and (max-width: 768px) {
      /* Styles for smaller screens */
    }

    @media screen and (min-width: 1200px) {
      /* Styles for larger screens */
    }
    ```

14. **Explain the concept of CSS specificity and how it affects style precedence.**
    - **Answer:** CSS specificity determines which styles take precedence when multiple conflicting styles are applied to the same element. It follows a hierarchy based on selectors' specificity.

15. **What is the purpose of the `transform` property in CSS3? Provide examples of its usage.**
    - **Answer:** The `transform` property in CSS3 is used to apply transformations like rotation, scaling, skewing, or translating elements. It is commonly used for animations and effects.

    ```css
    .box {
      transform: rotate(45deg);
      /* Other transform properties */
    }
    ```

16. **Explain the difference between `inline` and `inline-block` display properties in CSS.**
    - **Answer:** 
      - `inline` elements do not start on a new line and only take up as much width as necessary. They cannot have height or vertical margins.
      - `inline-block` elements start on a new line like block-level elements but can have width, height, and vertical margins.

17. **What is the purpose of the `object-fit` property in CSS3?**
    - **Answer:** The `object-fit` property specifies how an `<img>` or `<video>` element should be resized to fit its container. Values include `fill

`, `contain`, `cover`, `none`, `scale-down`.

    ```css
    img {
      object-fit: cover;
    }
    ```

18. **Explain the difference between `box-sizing: content-box;` and `box-sizing: border-box;` in CSS.**
    - **Answer:** 
      - `box-sizing: content-box;` calculates an element's width and height based on its content, excluding padding and border.
      - `box-sizing: border-box;` calculates an element's width and height including padding and border, but not margin.

    ```css
    .box {
      box-sizing: border-box;
      width: 100px;
      padding: 10px;
      border: 2px solid black;
    }
    ```

19. **What is the purpose of the `will-change` property in CSS3 and when should it be used?**
    - **Answer:** The `will-change` property hints to the browser that an element's property is expected to change, allowing the browser to optimize rendering. It should be used for properties that are going to be animated or transitioned.

    ```css
    .box {
      will-change: transform;
    }
    ```

20. **Explain the difference between `transition` and `animation` properties in CSS3.**
    - **Answer:** 
      - `transition` is used to smoothly change property values over a specified duration, triggered by a state change (e.g., hover).
      - `animation` allows creating complex animations with keyframes and timing functions, giving more control over the animation's behavior.

    ```css
    .box {
      transition: width 0.5s ease-in-out;
    }

    @keyframes slide-in {
      from { transform: translateX(-100%); }
      to { transform: translateX(0); }
    }

    .box {
      animation: slide-in 1s ease-in-out forwards;
    }
    ```

21. **What is the purpose of the `pointer-events` property in CSS3?**
    - **Answer:** The `pointer-events` property controls whether an element can be the target of pointer events like click or hover. Values include `auto`, `none`, `visible`, `visiblePainted`, `visibleFill`, `visibleStroke`, `all`.

    ```css
    .button {
      pointer-events: none; /* Disables pointer events on the button */
    }
    ```

22. **Explain the concept of CSS flexbox and provide examples of its properties.**
    - **Answer:** Flexbox is a layout model used for designing flexible and responsive layouts. Properties like `display: flex;`, `flex-direction`, `justify-content`, `align-items`, `flex-grow`, `flex-shrink`, `flex-basis` are commonly used.

    ```css
    .container {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    ```

23. **What is the purpose of the `outline` property in CSS and how does it differ from `border`?**
    - **Answer:** The `outline` property draws a line around an element, similar to `border`, but it does not take up space or affect layout. It is often used for highlighting elements.

    ```css
    .input:focus {
      outline: 2px solid blue;
    }
    ```

24. **Explain the concept of CSS grid layout and provide examples of its properties.**
    - **Answer:** CSS Grid Layout is a two-dimensional layout system used for creating grid-based layouts with rows and columns. Properties like `display: grid;`, `grid-template-columns`, `grid-template-rows`, `grid-gap`, `grid-column`, `grid-row` are commonly used.

    ```css
    .container {
      display: grid;
      grid-template-columns: 1fr 2fr;
      grid-gap: 10px;
    }
    ```

25. **What are pseudo-elements in CSS3 and provide examples of commonly used ones.**
    - **Answer:** Pseudo-elements are used to style specific parts of an element. Examples include `::before`, `::after`, `::first-line`, `::first-letter`, `::selection`.

    ```css
    p::before {
      content: '>>';
    }

    p::first-letter {
      font-size: 2em;
    }

    ::selection {
      background-color: yellow;
    }
    ```

26. **Explain the difference between `flex-grow`, `flex-shrink`, and `flex-basis` properties in CSS Flexbox.**
    - **Answer:** 
      - `flex-grow` specifies the ability of a flex item to grow relative to other items.
      - `flex-shrink` specifies the ability of a flex item to shrink relative to other items.
      - `flex-basis` specifies the initial size of a flex item before any remaining space is distributed.

    ```css
    .item {
      flex-grow: 1;
      flex-shrink: 0;
      flex-basis: 100px;
    }
    ```

27. **What is the purpose of the `backface-visibility` property in CSS3?**
    - **Answer:** The `backface-visibility` property controls whether the back face of an element is visible when rotated in 3D space. Values include `visible` and `hidden`.

    ```css
    .card {
      transform: rotateY(180deg);
      backface-visibility: hidden; /* Hides the back face */
    }
    ```

28. **Explain the difference between `transform: translate()` and `transform: translateX()` in CSS3.**
    - **Answer:** 
      - `transform: translate()` moves an element along the X and Y axes.
      - `transform: translateX()` moves an element only along the X axis.

    ```css
    .box {
      transform: translate(50px, 20px); /* Moves 50px right and 20px down */
    }

    .box {
      transform: translateX(50px); /* Moves 50px right */
    }
    ```

29. **What is the purpose of the `clip-path` property in CSS3?**
    - **Answer:** The `clip-path` property clips an element to a specific shape or path. It is commonly used for creating non-rectangular shapes or masking elements.

    ```css
    .image {
      clip-path: polygon(0 0, 100% 0, 100% 70%, 50% 100%, 0 70%);
    }
    ```

30. **Explain the concept of CSS transitions and provide examples of properties that can be transitioned.**
    - **Answer:** CSS transitions allow smooth animations when property values change. Properties like `color`, `background-color`, `opacity`, `transform`, `width`, etc., can be transitioned.

    ```css
    .box {
      transition: background-color 0.3s ease-in-out;
    }

    .box:hover {
      background-color: blue;
    }
    ```

31. **What is the purpose of the `mix-blend-mode` property in CSS3?**
    - **Answer:** The `mix-blend-mode` property defines how an element's

 content should blend with the content of its parent and background. Values include `normal`, `multiply`, `screen`, `overlay`, `darken`, `lighten`, etc.

    ```css
    .overlay {
      mix-blend-mode: screen;
    }
    ```

32. **Explain the difference between `overflow: hidden;` and `overflow: auto;` in CSS.**
    - **Answer:** 
      - `overflow: hidden;` hides content that overflows its container without adding scrollbars.
      - `overflow: auto;` adds scrollbars when content overflows the container, allowing users to scroll to see hidden content.

    ```css
    .container {
      overflow: hidden; /* Hides overflow content */
    }

    .scrollable {
      overflow: auto; /* Adds scrollbars if content overflows */
    }
    ```

33. **What is the purpose of the `mask-image` property in CSS3?**
    - **Answer:** The `mask-image` property applies an SVG mask to an element, defining areas where content is visible or hidden. It is used for creating complex shapes or effects.

    ```css
    .element {
      mask-image: url('mask.svg');
    }
    ```

34. **Explain the difference between `background-size: cover;` and `background-size: contain;` in CSS.**
    - **Answer:** 
      - `background-size: cover;` scales the background image to cover the entire container, maintaining aspect ratio and possibly cropping parts of the image.
      - `background-size: contain;` scales the background image to fit within the container, maintaining aspect ratio and without cropping.

    ```css
    .container {
      background-image: url('image.jpg');
      background-size: cover; /* Image covers the container */
    }

    .container {
      background-image: url('image.jpg');
      background-size: contain; /* Image fits within the container */
    }
    ```

35. **What are CSS selectors and provide examples of different types of selectors.**
    - **Answer:** CSS selectors are used to target specific HTML elements for styling. Examples include element selectors, class selectors, ID selectors, attribute selectors, pseudo-classes, and pseudo-elements.

    ```css
    /* Element Selector */
    p {
      color: red;
    }

    /* Class Selector */
    .highlight {
      background-color: yellow;
    }

    /* ID Selector */
    #header {
      font-size: 24px;
    }

    /* Attribute Selector */
    input[type="text"] {
      border: 1px solid black;
    }

    /* Pseudo-class Selector */
    a:hover {
      text-decoration: underline;
    }

    /* Pseudo-element Selector */
    p::first-letter {
      font-size: 2em;
    }
    ```

36. **Explain the concept of CSS variables (custom properties) and provide examples of their usage.**
    - **Answer:** CSS variables allow storing reusable values in CSS. They are defined using the `--variable-name` syntax and accessed using the `var()` function.

    ```css
    :root {
      --primary-color: #007bff;
    }

    .button {
      background-color: var(--primary-color);
    }
    ```

37. **What is the purpose of the `filter` property in CSS3 and provide examples of its usage.**
    - **Answer:** The `filter` property applies graphical effects like blur, brightness, contrast, grayscale, etc., to elements. It is commonly used for image effects or visual enhancements.

    ```css
    .image {
      filter: grayscale(50%);
    }
    ```

38. **Explain the concept of CSS specificity and how it affects style precedence.**
    - **Answer:** CSS specificity determines which styles take precedence when multiple conflicting styles are applied to the same element. It follows a hierarchy based on selectors' specificity.

39. **What is the purpose of the `min()` and `max()` functions in CSS and provide examples of their usage.**
    - **Answer:** The `min()` and `max()` functions in CSS are used to set the minimum or maximum value for properties like width or height, based on available space or content.

    ```css
    .box {
      width: min(300px, 100%);
      /* Width will be 300px or 100% (whichever is smaller) */
    }

    .box {
      width: max(200px, 50%);
      /* Width will be 200px or 50% (whichever is larger) */
    }
    ```

40. **Explain the concept of CSS animation and provide examples of keyframes and animation properties.**
    - **Answer:** CSS animation allows creating animated effects using keyframes and animation properties like `animation-name`, `animation-duration`, `animation-timing-function`, `animation-delay`, `animation-iteration-count`, `animation-direction`, `animation-fill-mode`.

    ```css
    @keyframes slide-in {
      from { transform: translateX(-100%); }
      to { transform: translateX(0); }
    }

    .box {
      animation: slide-in 1s ease-in-out forwards;
    }
    ```

41. **What is the purpose of the `unicode-bidi` property in CSS3?**
    - **Answer:** The `unicode-bidi` property sets the direction of text content that is mixed-directional (contains both left-to-right and right-to-left text). Values include `normal`, `embed`, `override`, `isolate`, `plaintext`.

    ```css
    .rtl {
      unicode-bidi: embed;
      direction: rtl; /* Right-to-left text */
    }
    ```

42. **Explain the difference between `currentColor` and `inherit` keywords in CSS.**
    - **Answer:** 
      - `currentColor` represents the value of the element's `color` property and is used to inherit the current text color for other properties like borders or backgrounds.
      - `inherit` explicitly inherits the value of a property from its parent element.

    ```css
    .box {
      color: red;
      border: 2px solid currentColor; /* Border color will be red */
    }

    .child {
      color: inherit; /* Inherits color from parent */
    }
    ```

43. **What is the purpose of the `text-overflow` property in CSS3? Provide examples of its usage.**
    - **Answer:** The `text-overflow` property specifies how overflowed content in a text container should be displayed, especially when it's truncated. Values include `clip`, `ellipsis`, `string`.

    ```css
    .ellipsis {
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    ```

44. **Explain the difference between `rem` and `em` units in CSS.**
    - **Answer:** 
      - `rem` represents the font size of the root element (`html`), making it more predictable and easier to manage in complex layouts.
      - `em` represents the font size of the current element, relative to its parent's font size.

    ```css
    body {
      font-size: 16px; /* 1rem = 16px */
    }

    .box {
      font-size: 1.

5rem; /* 1.5rem = 24px */
      padding: 1em; /* 1em = 24px (if parent's font-size is 16px) */
    }
    ```

45. **What is the purpose of the `perspective` property in CSS3?**
    - **Answer:** The `perspective` property defines the depth of the 3D space for transformed elements. It is used in conjunction with 3D transforms like `rotateX()`, `rotateY()`, `rotateZ()`.

    ```css
    .box {
      transform: rotateY(180deg);
      perspective: 1000px; /* Depth of 3D space */
    }
    ```

46. **Explain the concept of CSS counters and provide examples of their usage.**
    - **Answer:** CSS counters are used to increment or decrement values for elements, often used for numbering lists or generating automatic content.

    ```css
    ol {
      counter-reset: section;
    }

    li::before {
      content: counter(section) '.';
      counter-increment: sect
