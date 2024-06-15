# The-ultimate-JavaScript-Cheatsheet


# **<span style="color: orange;">JavaScript Basics Cheatsheet</span>**

## **<span style="color: skyblue;">Variables and Constants</span>**

- **<span style="color: LightPink;">Variables:</span>** Used to store data that can be changed later.

    ```js
    // Declaring a variable using var
    var x = 10;
    
    // Declaring a variable using let
    let y = 20;
    
    // Variables can be reassigned
    x = 15;
    y = 25;
    ```

- **<span style="color: LightPink;">Constants:</span>** Used to store data that cannot be changed.

    ```js
    // Declaring a constant using const
    const z = 30;
    
    // Trying to reassign a constant will throw an error
    // z = 35; // This will throw an error
    ```

## **<span style="color: skyblue;">Data Types</span>**

- **<span style="color: LightPink;">Primitive Data Types:</span>**
  
  - **<span style="color: LightPink;">Number:</span>**
  
    ```js
    let num = 42;
    let pi = 3.14;
    ```

  - **<span style="color: LightPink;">String:</span>**
  
    ```js
    let str = "Hello, world!";
    ```

  - **<span style="color: LightPink;">Boolean:</span>**
  
    ```js
    let isTrue = true;
    let isFalse = false;
    ```

  - **<span style="color: LightPink;">Undefined:</span>**
  
    ```js
    let undefinedVar;
    ```

  - **<span style="color: LightPink;">Null:</span>**
  
    ```js
    let nullVar = null;
    ```

  - **<span style="color: LightPink;">Symbol (ES6):</span>**
  
    ```js
    let sym = Symbol('description');
    ```

- **<span style="color: LightPink;">Reference Data Types:</span>**
  
  - **<span style="color: LightPink;">Object:</span>**
  
    ```js
    let person = {
      name: "John",
      age: 30
    };
    ```

  - **<span style="color: LightPink;">Array:</span>**
  
    ```js
    let arr = [1, 2, 3, 4, 5];
    ```

## **<span style="color: skyblue;">Operators</span>**

- **<span style="color: LightPink;">Arithmetic Operators:</span>**

    ```js
    let sum = 10 + 5;        // Addition
    let difference = 10 - 5; // Subtraction
    let product = 10 * 5;    // Multiplication
    let quotient = 10 / 5;   // Division
    let remainder = 10 % 3;  // Modulus
    let exponent = 2 ** 3;   // Exponentiation
    ```

- **<span style="color: LightPink;">Assignment Operators:</span>**

    ```js
    let a = 10;
    a += 5;  // a = a + 5
    a -= 5;  // a = a - 5
    a *= 5;  // a = a * 5
    a /= 5;  // a = a / 5
    a %= 3;  // a = a % 3
    a **= 2; // a = a ** 2
    ```

- **<span style="color: LightPink;">Comparison Operators:</span>**

    ```js
    let isEqual = (10 == "10");       // true (loose equality)
    let isStrictEqual = (10 === 10);  // true (strict equality)
    let isNotEqual = (10 != "10");    // false (loose inequality)
    let isStrictNotEqual = (10 !== 10); // false (strict inequality)
    let isGreater = (10 > 5);         // true
    let isLess = (10 < 5);            // false
    let isGreaterOrEqual = (10 >= 5); // true
    let isLessOrEqual = (10 <= 5);    // false
    ```

- **<span style="color: LightPink;">Logical Operators:</span>**

    ```js
    let andOperator = (true && false); // false
    let orOperator = (true || false);  // true
    let notOperator = (!true);         // false
    ```

- **<span style="color: LightPink;">Ternary Operator:</span>**

    ```js
    let result = (10 > 5) ? "Greater" : "Lesser"; // "Greater"
    ```

- **<span style="color: LightPink;">Type Operators:</span>**

    ```js
    let typeOfString = typeof "Hello"; // "string"
    let instanceOfObject = {} instanceof Object; // true
    ```

## **<span style="color: skyblue;">Control Structures</span>**

### **<span style="color: LightPink;">Conditionals</span>**

- **<span style="color: LightPink;">if-else:</span>**

    ```js
    let age = 18;
    
    if (age >= 18) {
      console.log("You are an adult.");
    } else {
      console.log("You are a minor.");
    }
    ```

- **<span style="color: LightPink;">if-else if-else:</span>**

    ```js
    let score = 85;
    
    if (score >= 90) {
      console.log("Grade: A");
    } else if (score >= 80) {
      console.log("Grade: B");
    } else if (score >= 70) {
      console.log("Grade: C");
    } else {
      console.log("Grade: F");
    }
    ```

- **<span style="color: LightPink;">switch:</span>**

    ```js
    let day = 3;
    
    switch (day) {
      case 1:
        console.log("Monday");
        break;
      case 2:
        console.log("Tuesday");
        break;
      case 3:
        console.log("Wednesday");
        break;
      case 4:
        console.log("Thursday");
        break;
      case 5:
        console.log("Friday");
        break;
      case 6:
        console.log("Saturday");
        break;
      case 7:
        console.log("Sunday");
        break;
      default:
        console.log("Invalid day");
    }
    ```

### **<span style="color: LightPink;">Loops</span>**

- **<span style="color: LightPink;">for loop:</span>**

    ```js
    for (let i = 0; i < 5; i++) {
      console.log("Iteration:", i);
    }
    ```

- **<span style="color: LightPink;">while loop:</span>**

    ```js
    let i = 0;
    
    while (i < 5) {
      console.log("Iteration:", i);
      i++;
    }
    ```

- **<span style="color: LightPink;">do-while loop:</span>**

    ```js
    let i = 0;
    
    do {
      console.log("Iteration:", i);
      i++;
    } while (i < 5);
    ```


# **<span style="color: orange;">JavaScript Functions Cheatsheet</span>**

## **<span style="color: skyblue;">Functions</span>**

### **<span style="color: LightPink;">Function Declarations</span>**
- **<span style="color: LightPink;">Description:</span>** Defines a named function that can be called later.

    ```js
    function greet(name) {
      return `Hello, ${name}!`;
    }

    console.log(greet("Alice")); // Output: Hello, Alice!
    ```

### **<span style="color: LightPink;">Function Expressions</span>**
- **<span style="color: LightPink;">Description:</span>** Defines a function as part of a larger expression, typically assigned to a variable.

    ```js
    const greet = function(name) {
      return `Hello, ${name}!`;
    };

    console.log(greet("Bob")); // Output: Hello, Bob!
    ```

### **<span style="color: LightPink;">Arrow Functions</span>**
- **<span style="color: LightPink;">Description:</span>** A shorter syntax for function expressions, does not have its own `this`, `arguments`, or `super`.

    ```js
    const greet = (name) => `Hello, ${name}!`;

    console.log(greet("Charlie")); // Output: Hello, Charlie!
    ```

### **<span style="color: LightPink;">Higher-Order Functions</span>**
- **<span style="color: LightPink;">Description:</span>** Functions that take other functions as arguments or return functions.

    ```js
    const greet = (name) => `Hello, ${name}!`;

    const sayHello = (func, name) => func(name);

    console.log(sayHello(greet, "Dana")); // Output: Hello, Dana!
    ```

### **<span style="color: LightPink;">Closures</span>**
- **<span style="color: LightPink;">Description:</span>** Functions that remember the environment in which they were created.

    ```js
    function createCounter() {
      let count = 0;
      return function() {
        count++;
        return count;
      };
    }

    const counter = createCounter();

    console.log(counter()); // Output: 1
    console.log(counter()); // Output: 2
    ```

### **<span style="color: LightPink;">IIFE (Immediately Invoked Function Expressions)</span>**
- **<span style="color: LightPink;">Description:</span>** Functions that are executed immediately after they are defined.

    ```js
    (function() {
      console.log("This is an IIFE");
    })(); // Output: This is an IIFE

    (function(name) {
      console.log(`Hello, ${name}!`);
    })("Eve"); // Output: Hello, Eve!
    ```



# **<span style="color: orange;">JavaScript Objects Cheatsheet</span>**

## **<span style="color: skyblue;">Objects</span>**

### **<span style="color: LightPink;">Creating Objects</span>**
- **<span style="color: LightPink;">Description:</span>** Objects in JavaScript are collections of key-value pairs.

    ```js
    // Object literal
    const person = {
      firstName: "John",
      lastName: "Doe",
      age: 30,
      greet: function() {
        return `Hello, my name is ${this.firstName} ${this.lastName}.`;
      }
    };

    console.log(person.firstName); // Output: John
    console.log(person.greet());   // Output: Hello, my name is John Doe.
    ```

### **<span style="color: LightPink;">Object Methods</span>**
- **<span style="color: LightPink;">Description:</span>** Functions stored as object properties.

    ```js
    const person = {
      firstName: "Jane",
      lastName: "Smith",
      greet: function() {
        return `Hello, my name is ${this.firstName} ${this.lastName}.`;
      }
    };

    console.log(person.greet()); // Output: Hello, my name is Jane Smith.
    ```

### **<span style="color: LightPink;">this Keyword</span>**
- **<span style="color: LightPink;">Description:</span>** Refers to the current object in a method or constructor.

    ```js
    const person = {
      firstName: "Alice",
      lastName: "Johnson",
      greet: function() {
        return `Hello, my name is ${this.firstName} ${this.lastName}.`;
      }
    };

    console.log(person.greet()); // Output: Hello, my name is Alice Johnson.
    ```

### **<span style="color: LightPink;">Prototypes and Inheritance</span>**
- **<span style="color: LightPink;">Description:</span>** Allows objects to inherit properties and methods from other objects.

    ```js
    // Constructor function
    function Person(firstName, lastName) {
      this.firstName = firstName;
      this.lastName = lastName;
    }

    // Adding a method using prototype
    Person.prototype.greet = function() {
      return `Hello, my name is ${this.firstName} ${this.lastName}.`;
    };

    const john = new Person("John", "Doe");
    console.log(john.greet()); // Output: Hello, my name is John Doe.
    ```

### **<span style="color: LightPink;">ES6 Classes</span>**
- **<span style="color: LightPink;">Description:</span>** Syntactical sugar over JavaScript's prototype-based inheritance.

    ```js
    // ES6 Class
    class Person {
      constructor(firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
      }

      greet() {
        return `Hello, my name is ${this.firstName} ${this.lastName}.`;
      }
    }

    const jane = new Person("Jane", "Smith");
    console.log(jane.greet()); // Output: Hello, my name is Jane Smith.
    ```



# **<span style="color: orange;">JavaScript Arrays Cheatsheet</span>**

## **<span style="color: skyblue;">Arrays</span>**

### **<span style="color: LightPink;">Creating Arrays</span>**
- **<span style="color: LightPink;">Description:</span>** Arrays in JavaScript store multiple values in a single variable.

    ```js
    // Array literal
    const fruits = ["Apple", "Banana", "Cherry"];

    console.log(fruits[0]); // Output: Apple
    ```

### **<span style="color: LightPink;">Array Methods</span>**
- **<span style="color: LightPink;">Description:</span>** Methods to manipulate arrays: forEach, map, filter, reduce, etc.

    ```js
	    // forEach: Executes a provided function once for each array element
	    fruits.forEach((fruit) => {
	      console.log(fruit);
	    });
	
	    // map: Creates a new array populated with the results of calling a provided function on every element
	    const fruitLengths = fruits.map((fruit) => fruit.length);
	    console.log(fruitLengths); // Output: [5, 6, 6]
	
	    // filter: Creates a new array with elements that pass a test
	    const filteredFruits = fruits.filter((fruit) => fruit.startsWith("A"));
	    console.log(filteredFruits); // Output: ["Apple"]
	
	    // reduce: Applies a function to reduce the array to a single value
	    const totalLength = fruits.reduce((total, fruit) => total + fruit.length, 0);
	    console.log(totalLength); // Output: 17
    ```



# **<span style="color: orange;">Advanced Topics</span>**

#### **<span style="color: LightPink;">Promises</span>**
- **<span style="color: LightPink;">Description:</span>** An object representing the eventual completion or failure of an asynchronous operation.

    ```js
    // Creating a promise
    const myPromise = new Promise((resolve, reject) => {
      let success = true;
      if (success) {
        resolve("Promise fulfilled!");
      } else {
        reject("Promise rejected.");
      }
    });

    // Using a promise
    myPromise
      .then((message) => {
        console.log(message); // Output: "Promise fulfilled!"
      })
      .catch((error) => {
        console.error(error);
      });
    ```

#### **<span style="color: LightPink;">Async/Await</span>**
- **<span style="color: LightPink;">Description:</span>** A syntactic sugar built on promises that allows writing asynchronous code in a synchronous manner.

    ```js
    // Using async/await
    async function fetchData() {
      try {
        let response = await fetch('https://api.example.com/data');
        let data = await response.json();
        console.log(data);
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    }

    fetchData();
    ```

#### **<span style="color: LightPink;">Error Handling (try, catch, finally)</span>**
- **<span style="color: LightPink;">Description:</span>** Structures for handling errors and executing cleanup code.

    ```js
    // Using try, catch, and finally
    try {
      let result = riskyOperation();
      console.log('Operation successful:', result);
    } catch (error) {
      console.error('Operation failed:', error);
    } finally {
      console.log('Cleanup code executed.');
    }

    function riskyOperation() {
      if (Math.random() > 0.5) {
        return 'Success!';
      } else {
        throw new Error('Failure!');
      }
    }
    ```

#### **<span style="color: LightPink;">Modules (import, export)</span>**
- **<span style="color: LightPink;">Description:</span>** A way to split code into reusable, independent files and load them as needed.

    ```js
    // Exporting a function from a module (export.js)
    export function greet(name) {
      return `Hello, ${name}!`;
    }

    // Importing and using a function in another file (import.js)
    import { greet } from './export.js';

    console.log(greet('Alice')); // Output: "Hello, Alice!"
    ```



# **<span style="color: orange;">DOM Manipulation</span>**

#### **<span style="color: LightPink;">Selecting Elements</span>**
- **<span style="color: LightPink;">Description:</span>** Methods to select elements from the DOM.

    ```js
    // Selecting an element by ID
    const elementById = document.getElementById('myElement');
    
    // Selecting elements by class name
    const elementsByClassName = document.getElementsByClassName('myClass');
    
    // Selecting elements by tag name
    const elementsByTagName = document.getElementsByTagName('div');
    
    // Selecting the first matching element
    const firstElement = document.querySelector('.myClass');
    
    // Selecting all matching elements
    const allElements = document.querySelectorAll('.myClass');
    ```

#### **<span style="color: LightPink;">Modifying Elements</span>**
- **<span style="color: LightPink;">Description:</span>** Methods to change content and attributes of DOM elements.

    ```js
    // Changing innerHTML
    elementById.innerHTML = '<p>New Content</p>';
    
    // Changing textContent
    elementById.textContent = 'New Text Content';
    
    // Changing style
    elementById.style.color = 'blue';
    
    // Adding a class
    elementById.classList.add('newClass');
    
    // Removing a class
    elementById.classList.remove('oldClass');
    
    // Setting an attribute
    elementById.setAttribute('data-custom', 'value');
    
    // Removing an attribute
    elementById.removeAttribute('data-custom');
    ```

#### **<span style="color: LightPink;">Event Handling</span>**
- **<span style="color: LightPink;">Description:</span>** Methods to handle user interactions and other events.

    ```js
    // Adding an event listener
    elementById.addEventListener('click', function() {
      console.log('Element clicked!');
    });

    // Removing an event listener
    function handleClick() {
      console.log('Element clicked!');
    }
    elementById.addEventListener('click', handleClick);
    elementById.removeEventListener('click', handleClick);

    // Event delegation
    document.body.addEventListener('click', function(event) {
      if (event.target.matches('.myClass')) {
        console.log('Delegated click event on', event.target);
      }
    });
    ```


# **<span style="color: orange;">Browser APIs</span>**

#### **<span style="color: lightgreen;">Fetch API</span>**
- **<span style="color: skyblue;">Description:</span>** A modern way to make network requests similar to XMLHttpRequest.

    ```js
    // Using Fetch API to get data
    fetch('https://api.example.com/data')
      .then(response => {
        if (!response.ok) {
          throw new Error('Network response was not ok ' + response.statusText);
        }
        return response.json();
      })
      .then(data => {
        console.log(data);
      })
      .catch(error => {
        console.error('There has been a problem with your fetch operation:', error);
      });

    // Using Fetch API with async/await
    async function fetchData() {
      try {
        let response = await fetch('https://api.example.com/data');
        if (!response.ok) {
          throw new Error('Network response was not ok ' + response.statusText);
        }
        let data = await response.json();
        console.log(data);
      } catch (error) {
        console.error('There has been a problem with your fetch operation:', error);
      }
    }

    fetchData();
    ```

#### **<span style="color: Lightgreen;">LocalStorage</span>**
- **<span style="color: LightPink;">Description:</span>** A way to store data on the client side that persists even after the browser is closed.

    ```js
    // Setting an item in LocalStorage
    localStorage.setItem('username', 'Alice');
    
    // Getting an item from LocalStorage
    const username = localStorage.getItem('username');
    console.log(username); // Output: "Alice"
    
    // Removing an item from LocalStorage
    localStorage.removeItem('username');
    
    // Clearing all items from LocalStorage
    localStorage.clear();
    ```

#### **<span style="color: Lightgreen;">SessionStorage</span>**
- **<span style="color: LightPink;">Description:</span>** A way to store data on the client side that persists only for the duration of the page session.

    ```js
    // Setting an item in SessionStorage
    sessionStorage.setItem('sessionID', '123456');
    
    // Getting an item from SessionStorage
    const sessionID = sessionStorage.getItem('sessionID');
    console.log(sessionID); // Output: "123456"
    
    // Removing an item from SessionStorage
    sessionStorage.removeItem('sessionID');
    
    // Clearing all items from SessionStorage
    sessionStorage.clear();
    ```







# **<span style="color: orange;">ES6+ Features</span>**

#### **<span style="color: lightgreen;">Template Literals</span>**
- **<span style="color: skyblue;">Description:</span>** Allows embedding expressions inside string literals.

    ```js
    const name = 'Alice';
    const greeting = `Hello, ${name}!`; // Output: "Hello, Alice!"
    console.log(greeting);
    ```

#### **<span style="color: lightgreen;">Destructuring</span>**
- **<span style="color: skyblue;">Description:</span>** Extracts values from arrays or properties from objects into distinct variables.

    ```js
    // Array destructuring
    const [a, b] = [1, 2];
    console.log(a); // Output: 1
    console.log(b); // Output: 2

    // Object destructuring
    const {name, age} = {name: 'Alice', age: 25};
    console.log(name); // Output: Alice
    console.log(age); // Output: 25
    ```

#### **<span style="color: lightgreen;">Spread and Rest Operators</span>**
- **<span style="color: skyblue;">Description:</span>** The spread operator (...) expands an array into its elements, while the rest operator collects multiple elements into an array.

    ```js
    // Spread operator
    const arr1 = [1, 2];
    const arr2 = [...arr1, 3, 4];
    console.log(arr2); // Output: [1, 2, 3, 4]

    // Rest operator
    function sum(...numbers) {
      return numbers.reduce((acc, curr) => acc + curr, 0);
    }
    console.log(sum(1, 2, 3)); // Output: 6
    ```

#### **<span style="color: lightgreen;">Default Parameters</span>**
- **<span style="color: skyblue;">Description:</span>** Allows setting default values for function parameters.

    ```js
    function greet(name = 'Guest') {
      return `Hello, ${name}!`;
    }
    console.log(greet()); // Output: "Hello, Guest!"
    console.log(greet('Alice')); // Output: "Hello, Alice!"
    ```

#### **<span style="color: lightgreen;">Arrow Functions</span>**
- **<span style="color: skyblue;">Description:</span>** Provides a shorter syntax for writing functions and does not bind its own `this`.

    ```js
    const add = (a, b) => a + b;
    console.log(add(2, 3)); // Output: 5

    const greet = name => `Hello, ${name}!`;
    console.log(greet('Alice')); // Output: "Hello, Alice!"
    ```

#### **<span style="color: lightgreen;">Let and Const</span>**
- **<span style="color: skyblue;">Description:</span>** `let` allows block-scoped variable declarations. `const` is used to declare constants that cannot be reassigned.

    ```js
    // Using let
    let count = 1;
    if (true) {
      let count = 2;
      console.log(count); // Output: 2
    }
    console.log(count); // Output: 1

    // Using const
    const PI = 3.14;
    console.log(PI); // Output: 3.14
    // PI = 3.1415; // This will cause an error
    ```

# **<span style="color: orange;">TypeScript Basics</span>**

#### **<span style="color: lightgreen;">Types</span>**
- **<span style="color: skyblue;">Description:</span>** TypeScript provides static typing to JavaScript.

    ```ts
    let isDone: boolean = false;
    let count: number = 10;
    let username: string = 'Alice';
    let numbers: number[] = [1, 2, 3, 4];
    let tuple: [string, number] = ['Alice', 25];
    ```

#### **<span style="color: lightgreen;">Interfaces</span>**
- **<span style="color: skyblue;">Description:</span>** Defines the structure of an object.

    ```ts
    interface User {
      name: string;
      age: number;
      isAdmin?: boolean; // Optional property
    }

    const user: User = {
      name: 'Alice',
      age: 25
    };
    ```

#### **<span style="color: lightgreen;">Classes and Inheritance</span>**
- **<span style="color: skyblue;">Description:</span>** Supports object-oriented programming with classes and inheritance.

    ```ts
    class Person {
      name: string;
      age: number;

      constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
      }

      greet() {
        return `Hello, my name is ${this.name}`;
      }
    }

    class Employee extends Person {
      position: string;

      constructor(name: string, age: number, position: string) {
        super(name, age);
        this.position = position;
      }

      describe() {
        return `${this.greet()} and I am a ${this.position}`;
      }
    }

    const employee = new Employee('Alice', 25, 'Developer');
    console.log(employee.describe()); // Output: "Hello, my name is Alice and I am a Developer"
    ```

#### **<span style="color: lightgreen;">Modules</span>**
- **<span style="color: skyblue;">Description:</span>** Organizes code into reusable pieces.

    ```ts
    // module1.ts
    export const PI = 3.14;

    export function add(a: number, b: number): number {
      return a + b;
    }

    // module2.ts
    import { PI, add } from './module1';

    console.log(add(2, 3)); // Output: 5
    console.log(PI); // Output: 3.14
    ```




# **<span style="color: orange;">Miscellaneous</span>**

#### **<span style="color: lightgreen;">Regular Expressions</span>**
- **<span style="color: skyblue;">Description:</span>** Provides a way to match patterns within strings.

    ```js
    const regex = /hello/i;
    console.log(regex.test('Hello world')); // Output: true

    const match = 'Hello world'.match(regex);
    console.log(match[0]); // Output: "Hello"
    ```

#### **<span style="color: lightgreen;">Date and Time</span>**
- **<span style="color: skyblue;">Description:</span>** Provides functionality to work with dates and times.

    ```js
    const now = new Date();
    console.log(now); // Output: current date and time

    const specificDate = new Date('2024-01-01');
    console.log(specificDate); // Output: Mon Jan 01 2024...
    ```

#### **<span style="color: lightgreen;">Math Object</span>**
- **<span style="color: skyblue;">Description:</span>** Provides properties and methods for mathematical constants and functions.

    ```js
    console.log(Math.PI); // Output: 3.141592653589793
    console.log(Math.round(4.7)); // Output: 5
    console.log(Math.sqrt(16)); // Output: 4
    ```
