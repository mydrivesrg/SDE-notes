# Javascript:

### 1. **What is JavaScript?**
- JavaScript is high-level, interpreted programming language that is commonly used to add interactivity and dynamic behaviour to our web pages.
- It is widely known as the language of the web because it runs in web browsers and allows developers to create interactive elements, handle user input, and modify the content.
- Javascript is also can be used out of web browsers, such as in server-side environments with `Node.Js`, to build full-stack applications.
--------------------------------------------------------------------------------
### 2. **What is Hoisting? working with different variables?**
- Hoisting in Javascript refers to the process where variables and function declarations are `moved to the top` of their `containing scope`, during the `code execution time`.
- This means that regardless of where variables and functions are declared `within a scope`, they are treated as if they were declared at the `top of that scope`.

#### **For Variables declared with `var`:**
- Hoisting moves the `variable declaration` to the top of its `containing function or global scope`.
- However, the initialization (`assigning a value to the variable`) remains in its original place.
- This can sometimes lead to unexpected behaviour if variables are accessed before they are initialized.
- **It only moves `variable declaration` to the top, not `variable initialization`.**
- ```javascript
  console.log(myVar); //Output: undefined
  var myVar = "Hello, World!";
  console.log(myVar); //Output: Hello, World!
  ```
- 2
```
  console.log(n); // undefined 
  for(var i=0;i<10;i++){
    if(true){
      var n=212;
      console.log(n) // Output: 212
    }
  }
```

#### **For Variables declared with `let`:**
- For variables declared with `let`, hoisting works differently compared to `var`.
- With `let`, variables are hoisted to the top of their containing block, but unlike `var`, they are not initialized until the actual declaration statement is encountered in the code.
- **This means that with `let`, you cannot access the variable before it is declared.**
- ```javascript
  console.log(myVar); // Throws ReferenceError: myVar us not defined
  let myVar = "Hello, World!";
  console.log(myVar); // Output: Hello, World!
  ```
- Additionally, with `let`, hoisting occurs at the `block level` rather than the function or global level.
- **This means that variables declared with `let` inside blocks (`like loops and conditional statements`) are hoisted to the top of their respective blocks but are not accessible until the point of declaration.**

#### **For function Declarations:**
- Hoisting moves the `entire function declaration to the top` of its containing scope.
- This allows you to call functions before they are declared in the code.
- ```javascript
  sayHello();  //Output: Hello!

  function sayHello() {
    console.log("Hello");
  {
  ```

  - **IMP**
```javascript
  sayHello(); // ReferenceError: Cannot access 'sayHello' before initialization

  const sayHello=()=>{
    console.log("Hello")
  }

  sayHello() // Output: Hello
```
_______________________________________________________________________________________
### 3. **let vs var**
- Tha main differences betwwen `let` and `var` in JavaScript revolve around their `scoping behaviour` and `hoisting`.
#### **Scope:**
 - **`var`**: Variables declared with `var` are `function-scoped` or `global-scoped`.
 - This means they are visible throughout the function in which they are declared, even if declared within a block (like an `if` statement ot a loop).

 - **`let`**: Variables declared with `let` are block-scoped.
 - They are only accessible within the block(enclosed by curly braces) in which they are declared, including `if` statements, loops, and functions.

#### **Hoisting:**
 - **`var`**: Variables declared with `var` are hosted to the top of their `containing function or global scope`.
 - However, **Only declaration is hoisted, not the initialization.**

 - **`let`**: Variables declared with `let` are hoisted to the top of their containing block, but they are not initialized until the actual declaration statement is encountered in the code.
 - **Accessing `let` variables before their declaration results in a ReferenceError.**

#### **Redeclaration:**
 - **`var`**: Allows for variable redeclaration within the same scope.
 - Redeclaring a `var` variable within the same function or global scope will not throw an error.

 - **`let`**: Does not allow for variable redeclaration within the same scope.
 - Redeclaring a `let` variable with the same name within the same block scope(including nested blocks) will result in a `SyntaxError`.

#### **Global Scope:**
- **`var`**: Variables declared with `var` in the global scope become properties of global object(`window` in browser, `global` in Node js)

- **`let`**: Variables declared with `let` in the global scope do not become properties of the global object.
- They are scoped to the global scope but not attached as properties of the global object.



| Feature         | `let`                      | `var`                      | `const`                    |
|-----------------|-----------------------------|-----------------------------|-----------------------------|
| Scope           | Block-scoped               | Function-scoped / Global    | Block-scoped               |
| Hoisting        | Hoisted, but not initialized until declaration | Hoisted and initialized with undefined | Not hoisted               |
| Redeclaration   | Not allowed within the same scope | Allowed within the same scope | Not allowed within the same scope |
| Value Assignment| Can be reassigned           | Can be reassigned           | Cannot be reassigned        |
| Initialization  | Must be initialized before use | Can be used before initialization | Must be initialized before use |
| Global Object   | Not added to global object (`window` in browsers, `global` in Node.js) | Added to global object (`window` in browsers, `global` in Node.js) | Not added to global object (`window` in browsers, `global` in Node.js) |



##### Note: let and const were introduced in ES6.
_______________________________________________________________________________________
### 4. **Scope and Types?**
- **Scope:** Scope in programming refers to the `visibility` and `accessibility` of `variables` and `functions` within a particular part of the code.

#### Global Scope:
- Variables declared(any type) outside of any function or block have global scope.
- They are accessible from any part of the code, including inside functions and blocks.
- Variables declared with **`var`** in the global scope become properties of the global object(`window` in browser, `global` in Node js)
```javascript
 var globalVar = "I am a global variable";

 function myFunction() {
   console.log(globalVar);  // Accessible inside the function
 }

 console.log(globalVar);  // Accessible outside of the function
```
#### Function Scope:
- Variables declared inside a function have function scope.
- They are only accessible within the function in which they are declared.
- Variables declared with `var`,`let`, `const` in a function have function scope.
- Variables declared with **`var`** is hoisted to the top.
- **Variable declared without any keyword in function automatically assigned to the Global Scope.**
```javascript
function myFunction() {
  var localVar = "I am local variable";
  console.log(localVar); // Accessible inside the function
}
console.log(localVar); // Throws ReferenceError: localVar us not defined
```
#### Block Scope(ES6+):
- Variables declared with `let` or `const` inside a block(e.g., within curly braces `{}` of an `if` statement or a loop) have block scope.
- They are only accessible within that block and any nested blocks.
- Block-scoped variables[`let` and `const`] are not hoisted to the top of their containing block and arenot visible before their declarations.
```javascript
if(true) {
   let blockVar = "I am block variable";
   console.log(blockVar); // Accessible insode the block
}

console.log(blockVar); //Throws ReferenceError: blockVar is not defined
```
________________________________________________________________________________________________________________
________________________________________________________________________________________________________________
### 5. **Promises**
- A promise is a promise of code execution. The code either executes or fails, in both cases the subscriber will be notified.
- Promises in JavaScript are a way to handle asynchronous operations, such as `fetching data from server`, `reading files`, or `performing animations` without blocking the main thread.
- They provide a cleaner and more structured approach to dealing with asynchronous code compared to callbacks.
- Solution to callback hell and Pyramid of Domm.  

A promise represents the eventual completion or failure of an asynchronous operations, and it has three states:

- **PENDING**: The initial state of a promise. The operation is not yet completed or failed.
- **Fulfilled(Resolved)**: The state when the asynchronous operation is successfully completed.
- **Rejected:** The state when the asynchronous operation encounters an error or is unsuccessful.

To handle the result of a promise (either fulfilled or rejected), you can use `.then()` and `.catch()` methods:
- **`.then()`**: is used to handle the fulfillment of the promise.
- **`.catch()`**: is used to handle the rejection of the promise.

- Example:
```javascript
const myPromise = new Promise((resolve, reject)=>{
    const randomNumber = Math.random();

    if(randomNumber > 0.5){
        resolve(randomNumber); //
    } else {
        reject("Error: Random number is less than 0.5")
        
    }
});

myPromise.then((result)=>{
    console.log("Fulfilled: ",result);
})
.catch((error)=>{
    console.log("Rejected: ",error)
})
```

Callback hell is a situation in JavaScript where you end up with deeply nested callbacks within callbacks. It often happens when dealing with multiple asynchronous operations, like fetching data from a server or reading files. This nesting can make your code hard to read and understand, leading to maintenance issues and bugs. Imagine a staircase of functions inside functions inside functions—it's like getting lost in a maze of callbacks!
_______________________________________________________________________________________
### 6. **Promises vs Callback? relation?**
- A callback in Javascript is a function that is passed as an argument to another function and is executed after the completion of a particular task or operation.
- Callbacks are commonnly used in asynchronous programming to handle tasks that take time to complete, such as fetching data from server or reading file.

- Example of a Callback:
```javascript
  function fetchData(callback) {
    setTimeout(() => {
      const data = "Some data fetched from server";
      callback(data); // call the callback function with fetched data
    }, 2000); // Simulate a delay of 2 seconds
  }
  
  function processData(data){
    console.log("Processing Data: ", data)
  }
  
  fetchData(processData); // Pass the processData function as a callback
```
- In this example, `fetchData` is a function that simulates fetching data asynchronously(e.g., from a server) using `setTimeout`.
- It takes a callbacl function (`processData`) as an argument and callls it with the fetched data after a delay.

- **Comparison with Promises**
- Promises, on the other hand, are a more structured and modern approach to handling asynchronous operations in Javascript.
- They represent the eventual completion(fulfillment) or failure(rejection) of an asynchronous task and provide a cleaner way to manage asynchronous code compared to callbacks.
- **Promises offer several advantages over callbacks, such as `better error handling`, `earier chaining of asynchronous tasks`, and the ability to use `async/await` syntax for more readable code.

- **above same example with Promises:**
```javascript
function fetchData() { 
  return new Promise((resolve, reject)=>{
    setTimeout(() => {
        const data = "Some data fetched from server";
        resolve(data); // Resolve the promise with detched data
    }, 2000);  //Simulate a delay of 2 seconds
  });
}

function processData(data) {
    console.log("Processing Data:", data);
}

fetchData()
  .then(processData) //Use .then() to handle the fulfillment with process data
  .catch((error) => {
      console.log("Error:", error);
  });
```

### My own application example using both callback and Promise:
##### Callback:
```javascript
function fetchDataWithCallbacks(callback) {
    fetch('http://localhost:8080/api/getusers')
     .then(response => {
         if(!response.ok) {
             throw new Error('Network response was not ok');
         }
         return response.json();
     })
     .then(data => {
         callback(null, data);
     })
     .catch(error => {
         callback(error, null);
     });
}

function processDataWithCallback(error, data) {
    if(error) {
        console.log('Error fetching data:', error);
        return;
    }

    //Perform operations on received data
    console.log("Received Data:",data);
}

fetchDataWithCallbacks(processDataWithCallback);
```

##### Promise:
```javascript
function fetchDataWithPromises() { 
  return new Promise((resolve, reject)=>{
    fetch('http://localhost:8080/api/getusers')
      .then(response =>{
          if(!response.ok) {
              throw new Error('Network response was not ok');
          }
          return response.json();
      })
      .then(data => {
          resolve(data);
      })
      .catch(error => {
          reject(error);
      });
  });
}

function processData(data) {
    // Perform operations on received data
    console.log("Received data:", data);

    //Example operation: Filer using with age greater than 30
    const filteredUsers = data.filter(user => user.age >30);
    console.log("Filtered Users:", filteredUsers);
}

fetchDataWithPromises()
  .then(processData)
  .catch((error) => {
      console.log("Error fetching data:", error);
  });
```
_______________________________________________________________________________________
### 7. **Promise - is less than 10 rejected if more accepted, Write a promise for this**

##### Using Promises:

```javascript
function checkNumberWithPromise(number) {
  return new Promise((resolve, reject) => {
    if (number < 10) {
      resolve("Approved"); // Resolve with "Approved" if number is less than 10
    } else {
      reject("Rejected"); // Reject with "Rejected" if number is greater than or equal to 10
    }
  });
}

function handleApprovalWithPromise(result) {
  console.log("Promise result:", result);
}

function handleRejectionWithPromise(error) {
  console.error("Promise error:", error);
}

const numberToCheck = 8; // Example number to check

checkNumberWithPromise(numberToCheck)
  .then(handleApprovalWithPromise)
  .catch(handleRejectionWithPromise);
```

##### Using Callbacks:

```javascript
function checkNumberWithCallback(number, callback) {
  if (number < 10) {
    callback(null, "Approved"); // Call the callback with "Approved" if number is less than 10
  } else {
    callback("Rejected", null); // Call the callback with "Rejected" if number is greater than or equal to 10
  }
}

function handleResultWithCallback(error, result) {
  if (error) {
    console.error("Callback error:", error);
  } else {
    console.log("Callback result:", result);
  }
}

const numberToCheck = 12; // Example number to check

checkNumberWithCallback(numberToCheck, handleResultWithCallback);
```

________________________________________________________________________________________________________________

### 8. **Event loop - setTimeOut vs Promise which will take precede**
#### Event Loop: 
- The event loop is a crucial part of how Javascript handles asynchronous operations and maintains responsiveness in web applications.

- Overview how event loops works:
##### 1. Call Stack: 
- When you run JavaScript code, it is executed line by line in a single-threaded manner.
- As functions are called, they are added to the call stack.

##### 2. Asynchronous Operations:
- Javascript supports asynchronous operations, such as `setTimeout`, AJAX requests, and `Promises`.
- When an asynchronous operation is encountered, it is offloaded to the browser or runtime environment(e.g.,Node js) to be executed in the background.

##### Task Queue:
- Asynchronous operations, once completed, are placed in the taskqueue (also known as `callback queue` or `message queue`).
- Examples include `setTimeout`, DOM events.

##### Event loop:
- The event loop constantly checks two main queues: the `call stack` and the `task queue`.
- `If the call stack is empty and there are tasks in the task queue`, the event loop moves tasks from the `task queue to call queue`.

#### Simplified sequence of how the event loop processes tasks:
- Javascript code is executed line by line, adding functions to the `call queue`.
- When an asynchronous operation is encountered(e.g.,`setTimeout`), it is moved off the main thread and scheduled to be executed in the background.
- After the specified time or when the asynchronous operation completes, its callback is placed in the task queue.
- The event loop constantlt checks if the call stack is empty. if so, it takes tasks from the task queue to and moves them to the call stacks for execution.
- This process continous, allowing JavaScript to handle asynchronous tasks without blocking the main thread.

##### Event loop for Promises:

- Promises utilize microtasks, which are a separate queue with higher priority than regular tasks in the event loop.

Here's how the event loop works for promises:

1. **Promise Creation:** When a promise is created, its executor function starts executing immediately. This function typically contains asynchronous code, such as fetching data from a server.

2. **Asynchronous Execution:** When an asynchronous operation inside a promise (e.g., AJAX request, reading a file) is encountered, it is initiated and moves off the main thread.

3. **Promise State:** A promise has three possible states: pending, fulfilled, or rejected. Initially, a promise is in the pending state.

4. **Microtask Queue:** When a promise is resolved or rejected (i.e., its asynchronous operation completes), its `.then()` or `.catch()` callbacks are placed in the microtask queue.

5. **Event Loop:** The event loop constantly checks for tasks in the microtask queue after each cycle of the main event loop.

6. **Microtask Execution:** If the call stack is empty and there are microtasks in the microtask queue, the event loop processes them immediately, one by one, until the microtask queue is empty.

7. **Regular Task Queue:** Regular tasks, such as `setTimeout` callbacks, DOM events, or AJAX responses, are placed in the regular task queue (task queue or callback queue), which has lower priority than the microtask queue.

8. **Priority:** Microtasks have higher priority than regular tasks. This means that microtasks, including promise callbacks (`.then()` and `.catch()`), are executed before regular tasks in the event loop.

In summary, the event loop processes promises by placing their callbacks (`.then()` and `.catch()`) in the microtask queue, which has higher priority than regular tasks. This ensures that promise callbacks are executed as soon as possible after a promise is resolved or rejected, making promises ideal for handling asynchronous operations with predictable and ordered execution.

#### setTimeOut vs Promise which will take precede:
- Promises take precedence over `setTimeout` callbacks in the event loop because `promise callbacks are placed in **microtask queue**, which has higher priority than the `task queue` where `setTimeout` callbacks reside. 
________________________________________________________________________________________________________________
### 9. **setTimeOut vs setInterval**
- `setTimeout` and `setInterval` are two Javascript functions used for scheduling tasks to be executed after a certain delay or at regular intervals, respectively.

#### 1. setTimeout():
- the `setTimeout` function is used to execute a specific function or code block after specified delay in miliseconds.
- It takes two parameters: the function to be executed(or string containing code to be evaliated) and the delay in miliseconds
- After the delay alapses, the function or code block is added to the `task Queue` and executed when the `call stack` is empty(i.e., no synchronous code is running == single threaded== line by line)

```javascript
setTimeout(() => {
    console.log("Delayed execution after 2 seconds");
}, 2000);
```
#### setInterval();
- The `setInterval` function is used to repeatedly execute a specified function or code block at a defined interval(time period) in miliseconds.
- It takes two parameters: the function to be executed(or a string containg code to be executed) ad the interval in miliseconds betweem each execution.
- The function is executed repeatedly until `clearInterval` is called or the browser tab/ window is closed.
```javascript
const intervalId = setInterval(()=> {
    console.log("Repeated execution every after 3 seconds");
}, 3000)

// to stop the interval after a cetain time like 10 seconds
setTimeout(() => {
    clearInterval(intervalId);
    console.log("Interval Stopped after 10 seconds");
}, 10000);
```
________________________________________________________________________________________________________________
### 10. **Async and Await**
- `async` and `await` are features introduced in ECMAScript 2017(ES8) to simplify asynchronous code and make it more readable and maintainable.
- They work together to allow you to write asynchronous JavaScript code in synchronous-like manner, avoiding callback hell and improving code readability.

#### `async` Function:
- The `async` keyword is used to define asynchronous functions in Javascript.
- **An `async` function always returns a promise.**
- If the function explicitly returns a value, the promise will be resolved with that value.
- If the function throws an error, the promise will be rejected with that error.
- Inside an `async` function, you can use the `await` keyword to pause the execution of the function until a promise is resolved, making it wait for the asynchronous operation to complete.
- ```javascript
    async function fetchData() {
       // code
    }
  ```

#### `await` Keyword:
- The `await` keyword can only be used inside an `async` function.
- It pauses the execution  of `async` function until the primise passed to `await` is resolved or rejected.
- When used with a promise, `await` returns the resolved value of the promise. If the promise is rejected, an error is thrown, which can be caught using `try...catch`.
- `await` can be used with any promise-based asynchronous operation, such as `fetch`, `setTimeout`, `Promise`, etc.
```javascript
async function fetchData() {
   const response = await fetch('http://api.example.com/data');
   const data = await response.json();
   return data; 
}

// Calling the async function and handlin fthe returned promise
fetchData()
 .then(data => {
   console.log('Fetched data:', data); 
 })
 .catch(error => {
   console.error('Error fetched:', error);
  });
```

##### `async` function with multiple `await` statements, each awaiting a separate asynchronous operation:

```javascript
// Async function with multiple await statements
async function fetchDataWithAwait() {
  try {
    // Simulating fetching user data asynchronously
    const userResponse = await fetch('https://jsonplaceholder.typicode.com/users/1');
    if (!userResponse.ok) {
      throw new Error('Failed to fetch user data');
    }
    const userData = await userResponse.json();

    // Simulating fetching posts data asynchronously
    const postsResponse = await fetch('https://jsonplaceholder.typicode.com/posts?userId=1');
    if (!postsResponse.ok) {
      throw new Error('Failed to fetch posts data');
    }
    const postsData = await postsResponse.json();

    // Simulating additional asynchronous operation
    const additionalData = await fetch('https://jsonplaceholder.typicode.com/comments?postId=1')
      .then(response => response.json());

    // Combine and return the fetched data
    return {
      user: userData,
      posts: postsData,
      comments: additionalData
    };
  } catch (error) {
    throw new Error('Error fetching data: ' + error.message);
  }
}

// Function to display the fetched data
function displayFetchedData(data) {
  console.log('Fetched data:', data);
}

// Function to handle errors
function handleError(error) {
  console.error('Error:', error);
}

// Calling the async function and handling the returned promise
fetchDataWithAwait()
  .then(displayFetchedData)
  .catch(handleError);
```

In this example:

1. We define an `async` function named `fetchDataWithAwait` that demonstrates multiple asynchronous operations using `await`.
2. Inside `fetchDataWithAwait`, we have three separate `await` statements:
   - Fetching user data asynchronously.
   - Fetching posts data asynchronously.
   - Fetching additional data asynchronously using a `.then()` chain.
3. Each `await` statement pauses the execution of the function until the corresponding asynchronous operation is completed, making the code appear synchronous and easier to read.
4. We handle errors using `try...catch` blocks within the `async` function and throw custom error messages for failed asynchronous operations.
5. Finally, we call `fetchDataWithAwait` and handle the returned promise using `.then()` to display the fetched data or `.catch()` to handle errors.
________________________________________________________________________________________________________________
________________________________________________________________________________________________________________
### 11. **ES6 features you have used**  like arrow function, promise and more

In the example I provided, several ES6 (ECMAScript 2015) features are used. Here's a breakdown of the ES6 features used in the code:

1. **Arrow Functions (`() => {}`):**
   - Arrow functions are used throughout the code, such as in the `async` function, callback functions, and in the `.then()` chain.
   - Example: `const fetchDataWithAwait = async () => { ... };`

2. **Template Literals (``):**
   - Template literals are used for string interpolation, allowing variables and expressions to be embedded directly within a string using `${}`.
   - Example: ``throw new Error('Error fetching data: ' + error.message);``

3. **`let` and `const` Declarations:**
   - `let` and `const` are used for variable declarations, providing block-scoped variables (`let`) and constants (`const`).
   - Example: `const userResponse = await fetch('...');`

4. **Async/Await:**
   - `async` and `await` are used for asynchronous programming, allowing code to be written in a more synchronous style while handling promises.
   - Example: `async function fetchDataWithAwait() { ... }`

5. **Promises:**
   - Promises are used for asynchronous operations with `.then()` and `.catch()` to handle resolved and rejected states.
   - Example: `const additionalData = await fetch('...').then(response => response.json());`

6. **Fetch API:**
   - The Fetch API is used for making HTTP requests, such as fetching JSON data from a URL asynchronously.
   - Example: `const userResponse = await fetch('https://jsonplaceholder.typicode.com/users/1');`

7. **Object Destructuring:**
   - Object destructuring is used to extract specific properties from objects and assign them to variables.
   - Example: `const { userData } = await userResponse.json();`

8. **Promises with `.then()` Chain:**
   - Promises are used with `.then()` chaining to handle asynchronous operations and obtain data from resolved promises.
   - Example: `const additionalData = await fetch('...').then(response => response.json());`

______________________________________________________________________________________

### 12. **What is Rest Operatio**
- The rest operator (`...`) in Javascript is used to gather multiple elements into array.
- It allows you to represent an indefinite number of arguments as an array, making it useful for funstions that can accept a variable number of arguments.

- **Syntax:**
- The rest operator if denoted by three dots(`...`) followed by the parameter name in a function's parameter list.
- Syntax:
   ```javascript
     function functionName(...restParameter) { ... }
   ```
- **Usage:**
 - When a function is called with arguments, any additional arguments beyond the explicitly named parameters are collected into an array using the rest parameter.
 - The rest parameter must be the last parameter in the parameter lits, and there can be only one rest parameter in a function.

```javascript
function Sum(...numbers) {
    let total = 0;
    for(const number of numbers) {
        total += number;
    }

    return total;
}

console.log(Sum(1,2)) // outpue: 3
console.log(Sum(1,2,3,4)) // output: 10
console.log(Sum())  //output: 0
``` 
_______________________________________________________________________________________________
### 13. **Check is the String is Palindrome or not?**
- Brute Force
```javascript
function isPalindrome(name) {
    var copy = '';
    for(let i=name.length-1; i>=0;i--){
        copy+=name[i];
    }
    return copy == name;
}

console.log(isPalindrome("sds"))
```
- Optimized:
```javascript
function isPalindrome(str) {
    // Convert the String to lowercase and remove non alphanumeric numbers
    const cleanStr = str.toLowerCase().replace(/[^a-z0-9]/g,'');

    const reversedStr = cleanStr.split('').reverse().join('');

    return cleanStr == reversedStr;
}

console.log(isPalindrome("naan"))
```
_______________________________________________________________________________________________
### 14. **Do you know Array.reverse and Other Array functions in Js**
#### 1. `Array.reverse()`:
- The `reverse()` method reverses the order of elements in an array in place.
- The first element becomes the last, the second element becomes the second to last, and so on.
- ```javascript
  const fruits = ['apple','banana','cherry'];
  fruits.reverse(); //['cherry','banana','apple']

#### 2. `Array.forEach()`:
- The `forEach` method executes a provided function once for each array element.
- ```javascript
  const numbers = [1,2,3,4,5];
  number.forEach(number => console.log(number *2)); // Outputs: 2,4,6,8,10
  ```
#### 3. `Array.find()`:
- The `find()` method returns the first element in an array that satisfies a specified condition, or `undefined` if no such eleement is found.
- 

#### 4. Array.map()

The `Array.map()` method creates a new array by applying a function to each element of the original array. It doesn't modify the original array but returns a new array with the results of applying the provided function to each element.

- Example:

Suppose we have an array of numbers and we want to double each number in the array using `Array.map()`:

```javascript
const numbers = [1, 2, 3, 4, 5];

const doubled = numbers.map(number => number * 2);

console.log(doubled); // Output: [2, 4, 6, 8, 10]
```

In this example:
- `numbers.map()` creates a new array `doubled` by doubling each element of the `numbers` array using the arrow function `number => number * 2`.
- The result is a new array `[2, 4, 6, 8, 10]` where each number has been doubled.

#### 5. Array.filter()

The `Array.filter()` method creates a new array with elements that pass a certain condition specified by a callback function. It doesn't modify the original array but returns a new array with the elements that meet the condition.

##### Example:

Suppose we have an array of numbers and we want to filter out only the even numbers using `Array.filter()`:

```javascript
const numbers = [1, 2, 3, 4, 5];

const evenNumbers = numbers.filter(number => number % 2 === 0);

console.log(evenNumbers); // Output: [2, 4]
```

In this example:
- `numbers.filter()` creates a new array `evenNumbers` with only the elements that are even, using the arrow function `number => number % 2 === 0`.
- The result is a new array `[2, 4]` containing only the even numbers from the original array.

#### 6. Array.reduce()

The `Array.reduce()` method applies a function to each element of an array to reduce it to a single value. It iterates over the array, accumulating a result by calling the provided function for each element.

##### Example:

Suppose we have an array of numbers and we want to calculate the sum of all numbers using `Array.reduce()`:

```javascript
const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce((accumulator, currentValue) => accumulator + currentValue, 0);

console.log(sum); // Output: 15
```

In this example:
- `numbers.reduce()` calculates the sum of all numbers in the array using the arrow function `(accumulator, currentValue) => accumulator + currentValue`.
- The initial value of the accumulator is `0` specified as the second argument to `reduce()`.
- The result is the sum of all numbers in the array, which is `15`.

_______________________________________________________________________________________
### 15. **Map vs Reduce**


| Method       | Purpose                          | Parameters                    | Return Value                |
|--------------|----------------------------------|-------------------------------|-----------------------------|
| `Array.map()`| Transforms each array element    | `callbackFn(currentValue, index, array)` | New array with transformed elements |
| `Array.filter()` | Filters array elements based on a condition | `callbackFn(currentValue, index, array)` | New array with filtered elements |
| `Array.reduce()` | Reduces array to a single value | `callbackFn(accumulator, currentValue, index, array), initialValue` | Accumulated value or final result |

_______________________________________________________________________________________
### 16. **JSON(name and age)- using filter to sort the age and print the name and age of users who's age is more than 26**

To filter and sort JSON data based on age and print the name and age of users whose age is more than 26, you can use the `Array.filter()` method along with conditional logic. Here's an example:

```javascript
const users = [
  { name: 'Alice', age: 30 },
  { name: 'Bob', age: 25 },
  { name: 'Charlie', age: 28 },
  { name: 'David', age: 22 },
  { name: 'Eve', age: 32 }
];

// Filter users whose age is more than 26
const filteredUsers = users.filter(user => user.age > 26);

// Print name and age of filtered users
filteredUsers.forEach(user => {
  console.log(`Name: ${user.name}, Age: ${user.age}`);
});
```

In this example:

- We have an array of objects `users` containing `name` and `age` properties for each user.
- We use `Array.filter()` to filter the `users` array and create a new array `filteredUsers` containing only those users whose age is more than 26.
- The `filteredUsers` array is then iterated using `Array.forEach()` to print the name and age of each filtered user.

When you run this code, it will print the name and age of users whose age is more than 26:

```
Name: Alice, Age: 30
Name: Charlie, Age: 28
Name: Eve, Age: 32
```

These are the users whose age is more than 26 according to the filtered data.

_______________________________________________________________________________________
### 17. **Shallow copy vs Deep copy**

Shallow copy and deep copy are concepts related to copying objects or arrays in programming, particularly in languages like JavaScript.

#### 1. **Shallow Copy:**
   - A shallow copy creates a new object or array and copies the top-level structure of the original object or array.
   - If the original object or array contains nested objects or arrays, a shallow copy only copies references to those nested objects or arrays, not the nested objects or arrays themselves.
   - Modifying a nested object or array in a shallow copy will affect the original object or array because they share references to the same nested objects or arrays.

#### 2. **Deep Copy:**
   - A deep copy creates a completely new object or array and recursively copies all nested objects and arrays within the original object or array.
   - Each nested object or array in a deep copy is duplicated, creating a separate copy that is independent of the original nested objects or arrays.
   - Modifying a nested object or array in a deep copy does not affect the original object or array because they are separate copies with no shared references.

### Example:

Let's illustrate shallow copy and deep copy with an example in JavaScript using objects:

```javascript
// Original object with nested objects
const originalObject = {
  name: 'John',
  age: 30,
  address: {
    city: 'New York',
    country: 'USA'
  }
};

// Shallow copy (using Object.assign or spread operator)
const shallowCopy = { ...originalObject };
shallowCopy.address.city = 'Los Angeles'; // Modify nested object in shallow copy

console.log(originalObject.address.city); // Output: Los Angeles (changes affect original)

// Deep copy (using JSON.parse and JSON.stringify)
const deepCopy = JSON.parse(JSON.stringify(originalObject));
deepCopy.address.city = 'Chicago'; // Modify nested object in deep copy

console.log(originalObject.address.city); // Output: Los Angeles (original is not affected)
```

In this example:
- Shallow copy (`shallowCopy`) is created using the spread operator `{ ...originalObject }`. Modifying the nested `address` object in `shallowCopy` also affects the original object because they share a reference to the same nested object.
- Deep copy (`deepCopy`) is created using `JSON.parse(JSON.stringify(originalObject))`. Modifying the nested `address` object in `deepCopy` does not affect the original object because they are separate copies with no shared references.

It's important to choose between shallow copy and deep copy based on the requirements of your program to ensure the desired behavior when working with nested objects or arrays.

_______________________________________________________________________________________
### 18. **Do you know what is Closures**

Sure, let's explain closures in a simple and understandable way.

### What is a Closure?
- Ability of a child class to remember the variables of the parent class or scope.
A closure in JavaScript is like a backpack that a function carries around with it. This "backpack" contains all the variables that were in scope when the function was created, even if those variables are no longer in scope when the function is executed.

### How Does it Work?

1. **Function Inside a Function:**
When you have a function inside another function, the inner function forms a closure over the variables in the outer function.

2. **Variables in the Backpack:**
   Any variables defined in the outer function that are used in the inner function are kept in the closure's "backpack." This means the inner function still has access to those variables even after the outer function has finished executing.

### Example:

```javascript
function outerFunction() {
  const message = 'Hello';

  function innerFunction() {
    console.log(message); // Accessing 'message' from the outer function
  }

  return innerFunction;
}

const myClosure = outerFunction();
myClosure(); // Output: Hello
```

In this example:
- The `outerFunction` defines a variable `message` and declares an inner function `innerFunction`.
- `innerFunction` is returned from `outerFunction` and assigned to `myClosure`.
- When `myClosure` is executed (`myClosure()`), it still has access to the `message` variable, even though `outerFunction` has finished executing. This is because of the closure created by `innerFunction`.

### Why Are Closures Useful?

1. **Encapsulation:** Closures allow you to encapsulate variables and functions, keeping them private within a specific scope.
2. **Data Persistence:** Closures help maintain the state of variables even after the outer function has finished executing.
3. **Callback Functions:** Closures are commonly used in callback functions and event handlers to maintain context and access variables from outer scopes.

In essence, closures are a powerful concept in JavaScript that enables functions to "remember" the environment in which they were created, leading to more flexible and expressive code.

### 19. **Currying in JavaScript**

Currying in JavaScript is a technique where a function with multiple arguments is transformed into a sequence of nested functions, each taking a single argument. The curried function allows you to partially apply arguments and create new functions with fewer parameters. This technique is named after Haskell Curry, a mathematician who made significant contributions to the field of combinatory logic.

### Example without Currying:

```javascript
// Regular function with multiple arguments
function add(a, b, c) {
  return a + b + c;
}

// Calling the function with all arguments
console.log(add(1, 2, 3)); // Output: 6
```

### Example with Currying:

```javascript
// Curried function using nested functions
function add(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    };
  };
}

// Partial application using currying
const addWithCurrying = add(1)(2);

// Calling the curried function with the remaining argument
console.log(addWithCurrying(3)); // Output: 6
```

In the example with currying:
- The `add` function is transformed into a curried function by nesting three functions, each taking one argument (`a`, `b`, `c`).
- Partial application is demonstrated by calling `add(1)(2)`, which returns a new function expecting the final argument (`c`).
- Finally, the returned function is called with the remaining argument (`3`) to get the result.

Currying provides several benefits, including:
1. **Partial Application:** You can create reusable functions by partially applying arguments.
2. **Flexibility:** Curried functions allow for greater flexibility and composition.
3. **Currying Libraries:** Some JavaScript libraries provide utility functions for currying, making it easier to work with curried functions.

Overall, currying is a powerful technique that helps in creating more modular and reusable code by breaking down functions into smaller units with fewer arguments.

_______________________________________________________________________________________
### 21. **Different types of events in Javascript?**

In JavaScript, there are several types of events that are commonly used. Here are some of the main types of events:

1. **Mouse Events:**
   - `click`: Triggered when the mouse is clicked on an element.
   - `mouseover`: Triggered when the mouse pointer enters the area of an element.
   - `mouseout`: Triggered when the mouse pointer leaves the area of an element.
   - `mousemove`: Triggered when the mouse pointer is moved over an element.
   - `mousedown`: Triggered when a mouse button is pressed down on an element.
   - `mouseup`: Triggered when a mouse button is released over an element.

2. **Keyboard Events:**
   - `keydown`: Triggered when a key is pressed down.
   - `keyup`: Triggered when a key is released.
   - `keypress`: Triggered when a key is pressed and released.

3. **Form Events:**
   - `submit`: Triggered when a form is submitted.
   - `input`: Triggered when the value of an input field changes.
   - `focus`: Triggered when an element gains focus.
   - `blur`: Triggered when an element loses focus.

_______________________________________________________________________________________
### 22. **event listener in Js**

An event listener in JavaScript is a function that listens for and responds to events triggered on HTML elements or other sources, such as the browser window. Event listeners are used to handle user interactions, such as clicking a button, submitting a form, or resizing the browser window.

### How Event Listeners Work:

1. **Attaching Event Listeners:**
   - You can attach an event listener to an element using the `addEventListener()` method. This method takes two main parameters: the event type (e.g., `'click'`, `'submit'`, `'keyup'`) and a callback function to handle the event.

2. **Callback Function:**
   - The callback function specified in `addEventListener()` is executed when the event occurs. It can take an event object as a parameter, which contains information about the event (e.g., target element, event type).

3. **Event Handling:**
   - Inside the callback function, you can write code to respond to the event. This can include modifying the DOM, performing calculations, making API requests, or triggering other functions.

### Example:

```javascript
// Get a reference to the button element
const button = document.querySelector('#myButton');

// Add an event listener for the 'click' event
button.addEventListener('click', function(event) {
  // Prevent the default behavior of the button (e.g., form submission)
  event.preventDefault();

  // Log a message when the button is clicked
  console.log('Button clicked!');
});
```

In this example:
- We use `document.querySelector('#myButton')` to select a button element with the ID `myButton`.
- We attach an event listener to the button using `addEventListener('click', ...)` to listen for the `'click'` event.
- The callback function inside `addEventListener()` is executed when the button is clicked, logging a message to the console.

Event listeners are fundamental in web development for creating interactive and responsive user interfaces. They enable JavaScript code to react to user actions and events triggered by the browser.
_______________________________________________________________________________________

### 23. **Error handling in Javascript?**

Error handling in JavaScript involves managing and responding to errors that may occur during the execution of your code. JavaScript provides mechanisms for detecting, handling, and recovering from errors to ensure smooth and reliable application behavior. Here's an overview of error handling techniques in JavaScript:

### 1. **Types of Errors:**
   - **Syntax Errors:** These occur when there are mistakes in the code syntax, such as missing brackets or semicolons.
   - **Runtime Errors (Exceptions):** These occur during code execution, such as trying to access undefined variables or calling methods on null objects.
   - **Logical Errors:** These are not technically errors but result in unexpected behavior due to incorrect logic or algorithm implementation.

### 2. **Try...Catch Statement:**
   The `try...catch` statement is used to handle exceptions and errors in JavaScript.

   ```javascript
   try {
     // Code that may throw an error
     throw new Error('Custom error message');
   } catch (error) {
     // Handle the error
     console.error('An error occurred:', error.message);
   }
   ```

   - The `try` block contains the code that may throw an error.
   - If an error occurs within the `try` block, it is caught by the `catch` block, and you can handle the error within the `catch` block.

### 3. **Error Object:**
   The `Error` object is used to create custom error messages and handle exceptions.

   ```javascript
   try {
     throw new Error('Custom error message');
   } catch (error) {
     console.error('An error occurred:', error.message);
   }
   ```

   - You can create instances of the `Error` object with custom error messages using `new Error('message')`.

### 4. **Throw Statement:**
   The `throw` statement is used to throw custom errors or exceptions.

   ```javascript
   function divide(x, y) {
     if (y === 0) {
       throw new Error('Division by zero error');
     }
     return x / y;
   }

   try {
     const result = divide(10, 0);
     console.log('Result:', result);
   } catch (error) {
     console.error('An error occurred:', error.message);
   }
   ```

   - In this example, the `divide` function throws an error if the divisor `y` is zero.

### 5. **Finally Block:**
   You can use a `finally` block after `try...catch` to execute code regardless of whether an error occurred or not.

   ```javascript
   try {
     // Code that may throw an error
   } catch (error) {
     // Handle the error
   } finally {
     // Code to be executed regardless of errors
   }
   ```

   - The `finally` block is often used for cleanup tasks or closing resources.

By using these error handling techniques, you can improve the robustness and reliability of your JavaScript code by gracefully handling errors and preventing unexpected crashes or failures.

_______________________________________________________________________________________

### 24. **Prototype?**

In JavaScript, prototypes are a fundamental part of the language's object-oriented programming model. Every JavaScript object has a prototype, which is a reference to another object. Prototypes are used to implement inheritance and property delegation in JavaScript.

Here are key points about prototypes in JavaScript:

1. **Prototype Chain:**
   - JavaScript uses a prototype chain to look up properties and methods of objects. When you access a property or method on an object, JavaScript first checks if that property or method exists on the object itself. If not, it looks for it in the object's prototype, and if still not found, it continues up the prototype chain until it reaches the `Object.prototype`, which is the top-level prototype in JavaScript.

2. **Prototype Property:**
   - Each object in JavaScript has a `prototype` property that refers to its prototype object. You can access an object's prototype using the `Object.getPrototypeOf()` method or the `__proto__` property (though using `__proto__` directly is discouraged due to compatibility concerns).

3. **Constructor Functions:**
   - When you create objects using constructor functions or classes in JavaScript, the objects inherit properties and methods from their constructor's prototype. This allows for efficient memory usage and code reuse.

4. **Prototype-Based Inheritance:**
   - JavaScript uses prototype-based inheritance rather than classical inheritance. Objects inherit directly from other objects, rather than from classes or blueprints.

### Example:

```javascript
// Constructor function for creating Person objects
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// Adding a method to the Person prototype
Person.prototype.greet = function() {
  console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
};

// Creating a new Person object
const john = new Person('John', 30);

// Calling the greet method (inherited from the prototype)
john.greet(); // Output: Hello, my name is John and I am 30 years old.
```

In this example:
- We define a `Person` constructor function with `name` and `age` properties.
- We add a `greet` method to the `Person.prototype`, which all `Person` objects will inherit.
- When we create a new `Person` object (`john`), it inherits the `greet` method from its prototype.

Prototypes play a crucial role in JavaScript's object-oriented programming paradigm by enabling inheritance, property delegation, and code reusability.

_______________________________________________________________________________________

### 25. **ESLint ?**

ESLint is a popular open-source static code analysis tool for JavaScript. It is used to find and fix problems in JavaScript code, enforce coding style conventions, and ensure code consistency across projects and team members. ESLint helps developers write cleaner, more reliable code by detecting potential errors, identifying problematic patterns, and enforcing best practices.

Key features of ESLint include:

1. **Code Quality Checks:**
   - ESLint performs static analysis of JavaScript code to identify errors, potential bugs, and common programming mistakes.
   - It checks for syntax errors, variable usage, function declarations, undefined variables, and more.

2. **Coding Style Enforcement:**
   - ESLint enforces coding style guidelines and conventions to maintain consistent code formatting and readability.
   - It checks for indentation, spacing, line length, naming conventions, and other stylistic rules defined in configuration files.

3. **Customizable Rules:**
   - ESLint provides a wide range of built-in rules that can be customized or extended based on project requirements.
   - Developers can create custom rules or configure existing rules to suit specific coding standards and preferences.

4. **Integration with Development Tools:**
   - ESLint can be integrated into popular code editors and IDEs, such as Visual Studio Code, Sublime Text, Atom, and more.
   - It can also be integrated into continuous integration (CI) pipelines to automate code quality checks during development.

5. **Configuration Files:**
   - ESLint uses configuration files (e.g., `.eslintrc.js`, `.eslintrc.json`) to define rules, environments, plugins, and other settings for code analysis.
   - Configuration files allow developers to fine-tune ESLint behavior and apply consistent coding standards across projects.

Overall, ESLint is a powerful tool for improving code quality, maintaining code consistency, and fostering better collaboration within development teams. It helps developers catch errors early, adhere to coding standards, and write cleaner, more maintainable JavaScript code.
_______________________________________________________________________________________

## 26. What is lasy loading in Javascript?
- Lazy loading in Javascript is a technique used to postpone the loading of non-essential resources (such as images, scripts, or stylesheets) until they are needed.
- This can improve the initial loading time of a webpage, as only essential content is loaded upfront, and non essential content is loaded asychronously as the user interacts with the page.
- The primary goal of lazy loading is to improve the initial loading time and performance of web pages by only loading essential content upfront and deferring(postponing) the loading of non-essential content until its needed.
--------------------------------------------------------------------------------
## 27. 
