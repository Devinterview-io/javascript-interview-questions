# 100 Common JavaScript Interview Questions

<div>
<p align="center">
<a href="https://devinterview.io/questions/web-and-mobile-development/">
<img src="https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/github-blog-img%2Fweb-and-mobile-development-github-img.jpg?alt=media&token=1b5eeecc-c9fb-49f5-9e03-50cf2e309555" alt="web-and-mobile-development" width="100%">
</a>
</p>

#### You can also find all 100 answers here 👉 [Devinterview.io - JavaScript](https://devinterview.io/questions/web-and-mobile-development/javascript-interview-questions)

<br>

## 1. What are the _data types_ present in JavaScript?

JavaScript has **primitive** and **composite** data types.

### Primitive Data Types

- **Boolean**: Represents logical values of **true** or **false**.
- **Null**: Denotes the lack of a value.

- **Undefined**: Indicates a variable that has been declared but has not been assigned a value.

- **Number**: Represents numeric values, including integers and floats.

- **BigInt**: Allows for representation of integers with arbitrary precision.

- **String**: Encapsulates sequences of characters.

- **Symbol** (ES6): Provides a unique, immutable value.

### Composite Data Types

- **Object**: Represents a set of key-value pairs and is used for more complex data structures.
- **Function**: A callable object that can be defined using regular function syntax or using the `new Function()` constructor (rarely used).

### Notable Characteristics

- JavaScript is **dynamically-typed**, meaning the data type of a variable can change during the execution of a program.
- **Data type coercion** can occur, where values are implicitly converted from one type to another in specific contexts, such as during comparisons.
- Arithmetic operations, particularly when one of the operands is a string, can lead to **implicit type conversions**.
<br>

## 2. What is the difference between _null_ and _undefined_?

While both **null** and **undefined** represent "no value" in JavaScript, they are distinct in their roles and origins.

### Origin and Context

- **null** usually denotes an intentionally **absent** value, and developers can set a variable to null to signify the absence of an object or a value. For example, if an API call doesn't return data, you might set a variable to null.

- **undefined** typically indicates a variable that has been declared but not yet been assigned a value, or a property that doesn't exist on an object.

### Variable Initialization and Assignment

- Variables that haven't been assigned a value are `undefined` by default, unless explicitly set to `null`.
  ```javascript
  let foo; // undefined
  let bar = null; // null
  ```

### Function Arguments

- When a function is called, and the parameter isn't provided or its value is not set, the parameter is `undefined`. 
- **null** would instead be an explicit value provided as an argument.

### Object Properties

- If you try to access a property on an object that doesn't exist, the result is `undefined`.
  ```javascript
  let obj = {};
  console.log(obj.nonExistentProperty); // undefined
  ```

- **Null** can be used to clear a property value in an object that was previously set.
  ```javascript
  let obj = { prop: 'value' };
  obj.prop = null;
  ```

### The Equality Operation

- In JavaScript, **undefined** and **null** are treated as equal when using loose equality (==) but not strict equality (===).

### Use-Cases and Best Practices

- When you initialize a variable and are not ready to assign a meaningful value, it's more common to use **undefined** instead of **null** to indicate that the value isn't there yet.
- For example, if you declare a user object but don't have their details yet, you might keep it as `undefined`.

### Code Example

Here is the JavaScript code:

```javascript
let var1;
let var2 = null;

let object = {
  a: 1,
  b: undefined
};

function test(arg1, arg2) {
  console.log(arg1);  // undefined: not provided
  console.log(arg2);  // null: provided as such
}

function clearProperty(prop) {
  delete object[prop];
}

console.log(var1);     // undefined
console.log(var2);     // null
console.log(object.a); // 1
console.log(object.b); // undefined
console.log(object.c); // undefined

test();               // Both arguments are undefined
test(1, null);        // arg1 is 1, arg2 is null

clearProperty('b');  // Removes property 'b' from object
console.log(object.b); // undefined: Property 'b' was removed, not set to null
```
<br>

## 3. How does JavaScript handle _type coercion_?

**Type Coercion** in JavaScript refers to the automatic conversion of values from one data type to another.

### Explicit and Implicit Coercion

- **Explicit**: Achieved through methods such as `parseInt()`, `Number()`, and `toString()`.
- **Implicit**: Automatically occurs during operations or comparisons. For example, combining a string and a number in an addition results in the automatic conversion of the number to a string.

### Common Coercion Scenarios

1. **Arithmetic Operations**: Strings are coerced to numbers.
    - **Example**: `"5" - 3` evaluates to `2`, as the string is coerced to a number.
    
2. **Loose Equality (==)**: Data types are often modified for comparisons.
    - **Example**: `"4" == 4` is `true` due to string coercion before the comparison.

3. **Conditionals** (if and Ternary Operators): Truthiness or falsiness is determined.
    - **Example**: `if(1)` evaluates to `true` because `1` coerces to `true`.

4. **Logical Operators**: Non-boolean values are coerced to booleans.
    - **Example**: `"hello" && 0` evaluates to `0` because the truthy `"hello"` short-circuits the `&&` operation, and `0` coerces to `false`.
<br>

## 4. Explain the concept of _hoisting_ in JavaScript.

**Hoisting** is a JavaScript mechanism that involves moving variable and function declarations to the top of their containing scope **during the compile phase**. However, the assignments to these variables or the definitions of functions remain in place.

For instance, even though the call to `myFunction` appears before its definition, hoisting ensures that it doesn't cause an error.

### Hoisting in Action

Here's a Code Example:

```javascript
console.log(myVar); // Undefined
var myVar = 5;

console.log(myVar); // 5

// The above code is equivalent to the following during the compile phase:
// var myVar;
// console.log(myVar);
// myVar = 5;

console.log(sayHello()); // "Hello, World!"
function sayHello() {
    return "Hello, World!";
}

// The above code is equivalent to the following during the compile phase:
// function sayHello() {
//     return "Hello, World!";
// }
// console.log(sayHello());
```

### Why Hoisting Matters

Understanding hoisting can help you prevent certain unexpected behaviors in your code. For example, it can shed light on unexpected "undefined" values that might appear even after a variable is declared and initialized.

#### Global Scope and Hoisting

In the global scope, variables declared with `var` and functions are always hoisted to the top. For example:

```javascript
// During the compile phase, the following global declarations are hoisted:
// var globalVar;
// function globalFunction() {}

console.log(globalVar); // Undefined
console.log(globalFunction()); // "Hello, Global!"
var globalVar = "I am global Var!";
function globalFunction() {
    return "Hello, Global!";
}
```

#### Local Scope and Hoisting

Variables and functions declared in local scopes within functions are also hoisted to the top of their scope.

Here's a Code Example:

```javascript
function hoistingInLocalScope() {
    // These local declarations are hoisted during the compile phase:
    // var localVar;
    // function localFunction() {}

    console.log(localVar); // Undefined
    localVar = "I am a local var!";
    console.log(localFunction()); // "Hello, Local!"

    var localVar;
    function localFunction() {
        return "Hello, Local!";
    }
}
```

### Best Practices

To write clean, readable code, it's important to:

- Declare variables at the top of your scripts or functions to avoid hoisting-related pitfalls.
- Initialize variables before use, **regardless of hoisting**, to ensure predictable behavior.

### ES6 and Hoisting

With the introduction of `let` and `const` in ES6, JavaScript's behavior has adapted. Variables declared using `let` and `const` are still hoisted, but unlike `var`, they are **not initialized**.

Here's an Example:

```javascript
console.log(myLetVar); // ReferenceError: Cannot access 'myLetVar' before initialization
let myLetVar = 5;
```

### Constants and Hoisting

`const` and `let` behave similarly when hoisted, but their difference lies in the fact that `const` must be assigned a value at the time of declaration, whereas `let` does not require an initial value.

Here's an Example:

```javascript
console.log(myConstVar); // ReferenceError: Cannot access 'myConstVar' before initialization
const myConstVar = 10;

console.log(myLetVar); // Undefined
let myLetVar = 5;
```
<br>

## 5. What is the _scope_ in JavaScript?

**Scope** defines the accessibility and lifetime of variables in a program. In JavaScript, there are two primary types: **Global Scope** and **Local Scope**.

### Global Scope

Any variable declared **outside of a function** is in the global scope. These can be accessed from both within functions and from other script tags.

#### Example: Global Scope

Here is the JavaScript code:

```javascript
let globalVar = 'I am global';

function testScope() {
    console.log(globalVar); // Output: 'I am global'
}

testScope();
console.log(globalVar); // Output: 'I am global'
```

### Local Scope

Variables declared within a **function** (using `let` or `const` or prior to JavaScript ES6 with `var`) have local scope, meaning they are only accessible within that function.

#### Example: Local Scope

Here is the JavaScript code:

```javascript
function testScope() {
    let localVar = 'I am local';
    console.log(localVar); // Output: 'I am local'
}

// This statement will throw an error because localVar is not defined outside the function scope
// console.log(localVar);
```

### Block Scope

Starting from **ES6**, JavaScript also supports block scope, where variables defined inside code blocks (denoted by `{}` such as loops or conditional statements) using `let` or `const` are accessible only within that block.

#### Example: Block Scope

Here is the JavaScript code:

```javascript
function testScope() {
    let localVar = 'I am local';
    if (true) {
        let blockVar = 'I am local to this block';
        console.log(localVar, blockVar); // Both will be accessible
    }
    // This statement will throw an error because blockVar is not defined outside the block scope
    // console.log(blockVar);
}

testScope();
```
<br>

## 6. What is the difference between `==` and `===`?

**Strict equality** (`===`) in JavaScript requires both value and type to match, testing for more specific conditions and reducing the likelihood of unexpected results.

In contrast, the **abstract equality** comparison (`==`) can lead to type coercion, potentially causing counterintuitive outcomes.

While both comparison modes test value equality, `===` ensures an additional match of data type.

### Illustrative Example: Abstract vs. Strict Equality

- Abstract Equality: 
    - `5 == '5'` evaluates to `true` because JavaScript converts the string to a number for comparison.
- Strict Equality:
    - `5 === '5'` evaluates to `false` because the types are not the same.

### Key Considerations

- **Type Safety**: `===` is safer as it avoids unwanted type conversions.
- **Performance**: `===` can be faster, especially for simple comparisons, as it doesn't involve type coercion or additional checks.
- **Clarity**: Favoring `===` can make your code clearer and more predictable.

### Common Best Practices

- **Use Strict Equality by Default**: This approach minimizes unintended side effects.
- **Consider Type Coercion Carefully**: In specific cases or with proven understanding, `==` can be suitable, but be cautious about potential confusion.

### Code Example: Equality Operators

Here is the JavaScript code:

```javascript
// Abstract equality
console.log('5' == 5);      // true
console.log(null == undefined);  // true
console.log(0 == false);    // true

// Strict equality
console.log('5' === 5);     // false
console.log(null === undefined); // false
console.log(0 === false);   // false
```
<br>

## 7. Describe _closure_ in JavaScript. Can you give an example?

In JavaScript, **closures** enable a **function** to access its outer scope, retaining this access even after the parent function has finished executing. This mechanism provides a powerful tool for data encapsulation and privacy.

### Core Concept

When a **function** is defined within another function, it maintains a reference to the variables from the outer function, even after the outer function has completed execution and its local variables are typically no longer accessible.

### Key Components

1. **Outer Function (Parent function)**: It contains the inner functions or closures.
2. **Inner Function (Closure)**: Defined within the parent function, it references variables from the outer function.
3. **Lexical Environment**: The context where the inner function is defined, encapsulating the scope it has access to.

### Example: Password Generator

Consider a simple scenario of a function in charge of generating a secret password:

1. The outer function, `generatePassword`, defines a local variable, `password` and returns an inner function `getPassword`.
2. The inner function, `getPassword`, has exclusive access to the `password` variable even after `generatePassword` has executed.

Here is the JavaScript code:

```javascript
function generatePassword() {
  let password = '';
  const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
  const passwordLength = 8;
  for(let i = 0; i < passwordLength; i++) {
    password += characters.charAt(Math.floor(Math.random() * characters.length));
  }

  return function getPassword() {
      return password;
  };
}

const getPassword = generatePassword();

console.log(getPassword()); // Outputs the generated password.
```

In this example, `getPassword` still has access to the `password` variable after the `generatePassword` function has completed, thanks to the closure mechanism.

### Application

- **Data Privacy**: JavaScript design patterns like the Module and Revealing Module Patterns use closures to keep data private.

- **Timeouts and Event Handlers**: Closures help preserve the surrounding context in asynchronous operations such as `setTimeout` and event handlers.

### Pitfalls to Avoid

- **Memory Leakage**: If not used carefully, closures can cause memory leaks, as the outer function's variables continue to live in memory because of the closure link.
- **Stale Data**: Be mindful of shared variables that might change after a closure has been defined, leading to unexpected behavior.

### Browser Compatibility

The concept of closures is a fundamental aspect of the JavaScript language and is supported by all modern browsers and environments.
<br>

## 8. What is the '_this_ keyword' and how does its context change?

In JavaScript, the context of **`this`** refers to the execution context, typically an object that owns the function where `this` is used.

### 'this' in the Global Scope

In **non-strict** mode, `this` in the global scope refers to the `window` object. In **strict** mode, `this` is `undefined`.

### 'this' in Functions

In **non-arrow functions**, the value of `this` depends on how the function is **invoked**. When invoked:

- As a method of an object: `this` is the object.
- Alone: In a browser, `this` is `window` or `global` in Node.js. In strict mode, it's `undefined`.
- With `call`, `apply`, or `bind`: `this` is explicitly set.
- As a constructor (with `new`): `this` is the newly created object.

### 'this' in Arrow Functions

Arrow functions have a **fixed context** for `this` defined at **function creation** and are not changed by how they are invoked.

- They do **not have** their own `this`.
- They use the `this` from their surrounding lexical context (the enclosing function or global context).

### Code Example: Global Context

Here is the JavaScript code:

```javascript
// Main
let globalVar = 10;

function globalFunction() {
    console.log('Global this: ', this.globalVar);
    console.log('Global this in strict mode: ', this);
}

globalFunction();  // Output: 10, window or undefined (in strict mode)

// In Node.js, it will be different, because "window" is not defined. But "this" will refer to the global object.
```
<br>

## 9. What are _arrow functions_ and how do they differ from regular functions?

Let's look at the key features of **arrow functions** and how they differ from traditional functions in JavaScript.

### Arrow Functions: Key Features

- **Concise Syntax**:
  - Especially useful for short, one-liner functions.
  - No need for `function` keyword or **braces** if there's a single expression.  
  
- **Implicit Return**:
  - When there's no explicit `{ return ... ;}` statement, arrow functions return the result of the single expression inside.

- **`this` Binding**:
  - Does not have its **own `this`**. It's "inherited" from the surrounding (lexical) context. This feature is known as '**lexical scoping**'.

### Code Example: Standard Function vs. Arrow Function

Here is the JavaScript code:

```javascript
// Standard Function
function greet(name) {
  return "Hello, " + name + "!";
}

// Arrow Function
const greetArrow = name => "Hello, " + name + "!";
```

In the code above, `greet` is a standard function, while `greetArrow` is an arrow function, showcasing the difference in syntax and required keywords.

### When to Use Arrow Functions

- **Event Handlers**: Ideal for concise, inline event handling, where `this` context can be inherited from the lexical scope.

- **Callback Functions**: Useful for array methods like `map`, `filter`, and `reduce`.

- **Avoidance of `this` Redefinition**: When you want to maintain the surrounding context of `this` and avoid unintended redefinition.

### Code Example: Arrow Function and `this` Context

Here is the JavaScript code:

```javascript
// Using traditional functions
document.getElementById('myButton').onclick = function() {
  console.log('Button clicked:', this);  // Refers to the button element
};

// Using arrow functions
document.getElementById('myButton').onclick = () => {
  console.log('Button clicked:', this);  // Refers to the global/window object
};
```

In the arrow function example, the context of `this` does not refer to the button element, but to the global `window` object, because arrow functions do not have their own binding of `this`. Instead, they inherit `this` from their lexical scope, which in this case is the global context.
<br>

## 10. What are _template literals_ in JavaScript?

**Template literals** are a feature in modern JavaScript versions that offer a more flexible and readable way to work with strings. They are often referred to as "template strings".

### Key Features

- **Multiline Text**: Template literals support multiline strings without requiring escape characters or string concatenation with a `+` sign.
- **String Interpolation**: They enable the seamless embedding of JavaScript expressions within strings, using `${}`.

### Syntax

- **Single Versus Double Quotes**: For template literals, use backticks (\`) instead of single quotes ('') or double quotes ("").
- **Placeholder**: The `${expression}` placeholder within the backticks allows for variable and expression injection.

### Example:

```javascript
let name = "John";
let message = `Hi ${name}!`;

console.log(message);  // Output: "Hi John!"
```

### Benefits

- **Readability**: They can make code more understandable, especially when dealing with longer or complex strings, by keeping content closer to its intention.
- **Interpolation & Expression**: Template literals reduce verbosity and rendering logic when integrating dynamic data.

### Code Example: Multiline Text and String Interpolation

```javascript
// Regular String
let poem = "Roses are red,\nViolets are blue,\nSugar is sweet,\nAnd so are you.";

// Template Literal
let poemTemplate = `
  Roses are red,
  Violets are blue,
  Sugar is sweet,
  And so are you.
`;
```

### Browser Compatibility Concerns

Template literals are universally supported in modern browsers and are now considered a **core JavaScript feature**. However, they may not work in older browsers such as Internet Explorer without transpilation or polyfilling.
<br>

## 11. What is a _higher-order function_ in JavaScript?

A **higher-order function** in JavaScript is a function that can take other functions as arguments or can return functions. This feature enables functional programming paradigms such as `map`, `reduce`, and `filter`. Higher-order functions offer versatility and modularity, fostering streamlined, efficient code.

### Key Characteristics

- **First-class functions**: Functions in JavaScript are considered first-class, meaning they are a legitimate data type and can be treated like any other value, including being assigned to variables, stored in data structures, or returned from other functions.

- **Closure support**: Due to closures, a higher-order function can transport not just the enclosed data within the function definition, but also the lexical environment in which that data resides.

- **Dynamic code**: Because JavaScript allows functions to be dynamically constructed and named, they can be dynamically passed to higher-order functions.

### Practical Applications

- **Callback Execution**: Functions like `setTimeout` and `addEventListener` take a function as an argument and are thus higher-order.

- **Event Handling**: Many event-driven systems leverage higher-order functions for tasks such as event subscription and emission.

- **Iterative Operations**: The `map`, `filter`, and `reduce` functions in JavaScript operate on arrays and require functions to be passed, making them higher-order.

- **Code Abstraction**: Higher-order functions enable the encapsulation of repetitive tasks, promoting cleaner, more readable code.

### Code Example: Higher-order Functions

Here is the JavaScript code:

```javascript
// Simple higher-order function
function multiplier(factor) {
  return function(num) {
    return num * factor;
  };
}

// Invoke a higher-order function
const twice = multiplier(2);
console.log(twice(5));  // Output: 10

// Functional programming with higher-order functions
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(multiplier(2));  // [2, 4, 6, 8, 10]
const tripled = numbers.map(multiplier(3));  // [3, 6, 9, 12, 15]
```
<br>

## 12. Can functions be assigned as values to variables in JavaScript?

Yes, **JavaScript** supports first-class functions, meaning **functions can be treated as variables** and then assigned to other variables or passed as arguments to other functions.

Functions defined as regular functions or arrow functions are both first-class in JavaScript. 

### Practical Code Example

Here is the JavaScript code:

```javascript
// Define a function
function greet() {
  console.log('Hello!');
}

// Assign the function to a variable
let sayHello = greet;

// Call the function through the variable
sayHello();  // Output: "Hello!"

// Reassign the variable to a new function
sayHello = function() {
  console.log('Bonjour!');
};

// Call it again to see the new behavior
sayHello();  // Output: "Bonjour!"
```

### Practical Use Cases

- **Callbacks**: Functions can be passed as parameters to other functions.
  
- **Event Handling**: In web development, functions define how to respond to specific events, and these functions are often attached to event listeners.

- **Modular Development**: In programming patterns like the Module pattern, functions are defined within a scope and then returned, similar to variables.

- **Higher-Order Functions**: These functions operate on other functions, taking them as arguments or returning them, and are an essential part of many modern JavaScript libraries and frameworks.
<br>

## 13. How do _functional programming_ concepts apply in JavaScript?

**Functional Programming** (FP) concepts in JavaScript are a direct result of the language's first-class functions. Key FP principles, such as immutability, pure functions, and **declarative** style, play a crucial role.

### Core Concepts

#### First-Class Functions and Higher-Order Functions

JavaScript treats functions as first-class citizens, allowing them to be assigned to variables, passed as parameters, and returned from other functions. This feature is foundational to FP in the language.

#### Code Example:

Here is the JavaScript code:

```javascript
const sayHello = () => console.log('Hello!');
const runFunction = (func) => func();

runFunction(sayHello);  // Output: "Hello!"
```
<br>

## 14. What are _IIFEs_ (Immediately Invoked Function Expressions)?

The **Immediately Invoked Function Expression** (IIFE) design pattern employs an anonymous function that gets executed promptly after its definition.

Key characteristics of IIFEs include localized variable scopes and immediate activation upon interpreter parsing.

### Code Example: IIFE

Here is the JavaScript code:

```javascript
(function(){
    var foo = 'bar';
    console.log(foo);
})();
```

In this example, the function is enclosed within parentheses, ensuring the enclosed function is evaluated as an expression. Subsequently, it is invoked with a trailing pair of parentheses.

### Core Functions of IIFE

1. **Encapsulation**: Through lexical scoping, IIFEs safeguard variables from leaking into the global scope. This, in turn, averts unintended variable tampering in the global context.

2. **Data Hiding**: Internal functions or data can be hidden from external access, providing a mechanism for information concealment and access control.

3. **Initialization**: The IIFE structure is ideal for setting up initial conditions, like binding events or pre-processing data.

### Use Cases

- **Avoiding Variable Pollution**: When interfacing with libraries or inserting code snippets, IIFEs prevent global scope pollution.

- **Module Patterns**: IIFEs, in combination with **closures**, lay the groundwork for modular code organization by shielding private variables and functions.

### Modern Alternatives

With the introduction of ES6 and its `let` and `const` declarations, as well as block-scoped lexical environments, the necessity of IIFEs has reduced. Additionally, **arrow functions** provide a more concise method for defining immediately invoked functions.

### IIFE Variants

1. **Parentheses Invocation**: A pair of parentheses immediately invoke the enclosed function. While this approach is more extensive, it's devoid of self-documenting advantages.
    ```javascript
    (function(){
        console.log('Invoked!');
    })();
    ```

2. **Wrapping in Operators**: Similar to using parentheses for invocation, the `!`, `+`, or `-` operators are sometimes used for invoking clarity. For instance:
    ```javascript
    !function(){
        console.log('Invoked!');
    }();
    ```

3. **Named IIFE**: Though not as common, naming an IIFE can assist with self-referencing. This is most effective when the intention is to have a more comprehensive stack trace during debugging.
    ```javascript
    (function factorial(n){
        if (n <= 1) return 1;
        return n * factorial(n-1);
    })(5);
    ```

#### Caution on Minification

When leveraging IIFEs, exercise caution while using minifiers to shrink JavaScript files. Minification might lead to unintended outcomes, altering the previous scope expectations.
<br>

## 15. How do you create _private variables_ in JavaScript?

In JavaScript, encapsulating private state within an object can be achieved using a **closure**. This ensures the state is local to the object and not directly accessible from outside.

### How Closures Work

A **closure** allows a function to retain access to the **lexical environment** (the set of variable bindings at the point of function declaration) in which it was defined, even when the function is executed outside that lexical environment.

This means that any **inner function**, defined inside another function, has access to the **outer function's variables**, and that access is maintained even after the outer function has finished executing.

For example:
```javascript
function outerFunction() {
    let outerVar = 'I am outer';  // This variable is in the lexical environment of outerFunction

    function innerFunction() {
        console.log(outerVar);  // Accesses outerVar from the lexical environment of outerFunction
    }

    return innerFunction;
}

let myInnerFunction = outerFunction();
myInnerFunction();  // Logs: "I am outer"
```

Here, `innerFunction` retains access to `outerVar`.

### Practical Implementation with Constructor Functions and Modules

#### Constructor Functions

When defining a JavaScript **constructor function** with `function` and `new`, closure can be used to associate private state with each instance:

```javascript
function Gadget() {
    let secret = 'top secret';
    this.setSecret = function (value) {
        secret = value;
    };
    this.getSecret = function () {
        return secret;
    };
}

let phone = new Gadget();
phone.setSecret('new secret');
console.log(phone.getSecret());  // 'new secret'
```

In this example, `secret` is private to each `Gadget` instance, thanks to closure.

#### Modules

In modern JavaScript, **module patterns** combined with **immediately-invoked function expressions** (IIFE) are often used for encapsulation and data hiding.

- The **revealing module pattern** enables selective exposure of private members.

- The **IIFE pattern** immediately executes and returns the object to be assigned, effectively creating a module.

Here is the code:

```javascript
let myModule = (function () {
    let privateVariable = 'I am private';

    function privateMethod() {
        console.log('I am a private method');
    }

    return {
        publicMethod: function () {
            console.log('I am a public method');
        },
        getPrivateVariable: function () {
            return privateVariable;
        }
    };
})();

console.log(myModule.getPrivateVariable());  // 'I am private'
myModule.privateMethod();  // Throws an error because privateMethod is not exposed
```

In this example, `privateVariable` and `privateMethod` are accessible only within the IIFE's lexical environment, thus making them private.

JavaScript tools like TypeScript and Babel also offer modules such as `module.export`, providing additional options for encapsulation.
<br>



#### Explore all 100 answers here 👉 [Devinterview.io - JavaScript](https://devinterview.io/questions/web-and-mobile-development/javascript-interview-questions)

<br>

<a href="https://devinterview.io/questions/web-and-mobile-development/">
<img src="https://firebasestorage.googleapis.com/v0/b/dev-stack-app.appspot.com/o/github-blog-img%2Fweb-and-mobile-development-github-img.jpg?alt=media&token=1b5eeecc-c9fb-49f5-9e03-50cf2e309555" alt="web-and-mobile-development" width="100%">
</a>
</p>

