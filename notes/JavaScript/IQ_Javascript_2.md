# Javascript -- II
----------------------------------------------------------------------------------
## 1. Lexical Scope:
- Lexical scope, also known as static scope, is a concept in Javascript that determines the accessibility of variables and functions based on their location within the code.
- code in one scope can access variables in same scope or any scope outside of it.

-------------------------------------------------------
## 2. Undefined and Null:
- both are primitive values.

### undefined:
- `undefined` typically means a variable has been declared but has not been assigned a value yet.
- Javascript automatically initializes variables to `undefined` when they are declared but not assigned a value.
- It can also occur as the default return value of a function if no explicit return value is specified.

```java
let x;
console.log(x);  // Output: undefined

function foo() {}
console.log(foo());
```
### null:
- `null` represents the intentional absence of any object value.
- it is often used to explicitly signify that a variable, object property, or function argument does not have a value.

```java
let y;
console.log(y):  // undefined
y = null;
console.log(y); // null
```

#### Type of undefined and null:

 - **Type of undefined is `undefined`.**
 - **Type of `null` is `object`.**
 - ```java
     console.log(typeof undefined)
     console.log(typeof null)
   ```
-----------------------------------------------------------------------------
## 3. typeof
```java
console.log(typeof ("22"+3))  // String
console.log(typeof ("22"-3))  //number
console.log(typeof ("22"%3))  // number
console.log(typeof ("22"*3))  // number
console.log(typeof ("22"/3))  // number
```
-----------------------------------------------------------
## 4. Javascript is static type or dynamic type language:
- Javascript is a dynamically typed language.
- This means that variable types are not explicitly declared in the code, and the type of a variable can change over the course of the program's execution.
- In dynamically typed langiages like javascript, variable types are determined at runtime based on the value assigned to them.
```java
let x = "Satish";
console.log(typeof x) // String
x = 23;
console.log(typeof x)  // numebr
x = false;
console.log(typeof x)  // boolean
```
---------------------------------------------------------------
## 5. polyfill in Javascript:
- Polyfill JS is some script code that provides the ability to support modern functionality on older versions of the web browser.
- Firstly understand the scope and meaning of the polyfills; Poly means it could be solved using multiple methods and not limited to just a JavaScript native approach, and fill means that it will fulfill the user's requirement and close the gap between the different browsers regardless of the technology.
- Essentially, polyfills enable the use of newer features in JavaScript on browsers that have not yet implemented those features.

- For example, let's create a polyfill for the `Array.prototype.map` method, which is a build-in method in modern Javascript engines but may not be available in very old browsers.


Here's how you can write a polyfill for `Array.prototype.map`:

```javascript
// Check if Array.prototype.map is not already defined
if (!Array.prototype.map) {
    // Define the polyfill
    Array.prototype.map = function(callback, thisArg) {
        // Check if the 'this' context is null or undefined
        if (this == null) {
            throw new TypeError('Array.prototype.map called on null or undefined');
        }

        // Ensure the callback is a function
        if (typeof callback !== 'function') {
            throw new TypeError(callback + ' is not a function');
        }

        // Convert 'this' to an object and get the length
        var O = Object(this);
        var len = O.length >>> 0;

        // Create a new array to store the results
        var result = new Array(len);

        // Iterate over the elements of the array
        for (var k = 0; k < len; k++) {
            if (k in O) {
                // Call the callback function for each element
                result[k] = callback.call(thisArg, O[k], k, O);
            }
        }

        // Return the new array
        return result;
    };
}

// Example usage:
var numbers = [1, 2, 3, 4, 5];
var doubled = numbers.map(function(number) {
    return number * 2;
});

console.log(doubled); // Output: [2, 4, 6, 8, 10]
```

Explanation of the polyfill:
1. **Check for Existing Method**: The polyfill first checks if `Array.prototype.map` is already defined. If it is not, the polyfill defines it.
2. **Type and Length Checks**: The polyfill ensures that the method is called on a valid array and that the provided callback is a function.
3. **Callback Execution**: It iterates over the array, applies the callback function to each element, and stores the results in a new array.
4. **Return Result**: Finally, it returns the new array containing the results of the callback function.

### Why Use Polyfills?
- **Browser Compatibility**: They help ensure that your code works across different browsers, including older ones.
- **Future-Proofing**: Using polyfills allows you to use modern JavaScript features without worrying about browser support.

### How to Use Polyfills
Polyfills can be included in your code directly, as shown above, or you can use libraries like [core-js](https://github.com/zloirock/core-js) that provide a comprehensive set of polyfills for modern JavaScript features. Including a polyfill library can be as simple as adding a script tag to your HTML or installing the library via a package manager like npm.

-----------------------------------------------------------
## 6. Falsy and truthy Values;
- **Falsy values are values that evaluate to `false` in the boolean context. **
- **Other falsy values are *`false`*, *`0`*, *`""(empty string)`*, *`undefined`*, *`null`* and *`Nan`***.

#### 1. null?console.log(1):console.log(2)
- Above is the ternary operatior in Javascript.
- **`null`** in javascript is a falsy value. so that it will print "2" in the console.

#### undefined == null and undefined === null?
- According to the Javascript specification, `undefined` and `null` are considered equal when using the `==` operator.
- **undefined == null ==>> return `true`**
- Since `undefined` and `null` are different types (`undefined` is of type `undefined`, and `null` is of type `object`), they are not considered equal when using the `===` operator.
- **undefined === null ==>> returns false**

```java
// falsy and truthy values

// falsy
console.log("Falsy Values:")
undefined?console.log(1):console.log(2)
null?console.log(1):console.log(2)
""?console.log(1):console.log(2)
0?console.log(1):console.log(2)

console.log("==============")

console.log("Truthy Values:")
1?console.log(1):console.log(2)       // Non zero is refers to true in context of boolean
-1?console.log(1):console.log(2)       // Non zero is refers to true in context of boolean
45?console.log(1):console.log(2)       // Non zero is refers to true in context of boolean
"name"?console.log(1):console.log(2)  // non-empty string

// Objects refers to true
const pairs = {key: 'value'}
pairs?console.log(1):console.log(2)  // non-empty string

const arr = []
arr?console.log(1):console.log(2)  // non-empty string
```
-------------------------------------------------------------------------------
## 7. how our jsx is rendered is the file is JavaScript?

In React, JSX (JavaScript XML) is a syntax extension that allows you to write HTML-like code within JavaScript. However, browsers do not understand JSX directly. React uses a process called transpilation to convert JSX into regular JavaScript code that browsers can execute. Here's an overview of how this works:

### How JSX is Rendered in React

1. **JSX Syntax**:
   - JSX allows you to write HTML-like syntax within JavaScript:
     ```jsx
     const element = <h1>Hello, world!</h1>;
     ```

2. **Transpilation with Babel**:
   - Before the code reaches the browser, a tool like Babel transpiles the JSX into JavaScript. Babel is a JavaScript compiler that transforms modern JavaScript features (like JSX) into code that browsers can understand.
   - The JSX code:
     ```jsx
     const element = <h1>Hello, world!</h1>;
     ```
     is transformed into:
     ```javascript
     const element = React.createElement('h1', null, 'Hello, world!');
     ```

3. **React.createElement()**:
   - The `React.createElement` function creates a JavaScript object called a React element. This object describes a DOM node and its attributes.
   - The signature of `React.createElement` is:
     ```javascript
     React.createElement(type, [props], [...children])
     ```
   - In the example above:
     ```javascript
     const element = React.createElement('h1', null, 'Hello, world!');
     ```
     - `type` is `'h1'` (indicating an HTML `h1` element).
     - `props` is `null` (no attributes).
     - `children` is `'Hello, world!'` (the content of the element).

4. **Rendering with ReactDOM**:
   - ReactDOM is the library that takes care of updating the DOM to match the React elements.
   - To render a React element into the DOM, you use the `ReactDOM.render` method:
     ```javascript
     ReactDOM.render(element, document.getElementById('root'));
     ```
   - This method takes a React element and a DOM container, and it updates the DOM to match the React element.

### Example in Context

Here’s a complete example that demonstrates this process:

1. **JSX Code**:
   ```jsx
   import React from 'react';
   import ReactDOM from 'react-dom';

   const element = <h1>Hello, world!</h1>;

   ReactDOM.render(element, document.getElementById('root'));
   ```

2. **Transpiled JavaScript Code** (using Babel):
   ```javascript
   import React from 'react';
   import ReactDOM from 'react-dom';

   const element = React.createElement('h1', null, 'Hello, world!');

   ReactDOM.render(element, document.getElementById('root'));
   ```

3. **Rendered HTML**:
   - After `ReactDOM.render` runs, the actual HTML in the browser would look like:
     ```html
     <div id="root">
       <h1>Hello, world!</h1>
     </div>
     ```

### Key Points:

- **JSX is syntactic sugar**: JSX makes it easier to write and visualize the structure of the UI components, but it is not necessary to use JSX with React. You can write plain JavaScript using `React.createElement`.
- **Transpilation**: Tools like Babel are essential for converting JSX into JavaScript that browsers can execute.
- **React Element**: The `React.createElement` function is central to creating elements that describe what you want to see on the screen.
- **ReactDOM**: The `ReactDOM.render` function is responsible for rendering the React element into the actual DOM and keeping it in sync with React's virtual DOM.

---------------------------------------------
