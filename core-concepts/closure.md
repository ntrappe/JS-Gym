# Closure

1. [Definition](#definition)
2. [Practical Uses](#practical-uses-of-closures)
3. [Knowledge Check](#knowledge-check)

## Definition
A **closure** is created when a function "remembers" the variables from its **lexical scope** even 
when the function is executed outside of that scope. It allows functions to access variables from
their enclosing scope even after the enclosing function has returned.

### Basic Example of a Closure
```js
function outerFunction() {
    let outerVariable = 'I am outside!';

    function innerFunction() {
        console.log(outerVariable); // The inner function can access outerVariable
    }

    return innerFunction;
}

const closure = outerFunction();
closure(); // Output: 'I am outside!'
```

## Practical Uses of Closures
### Emulating Private Variables
You can create **private variables** that can only be accessed or modified by specific functions. For example, we can call `increment` and `decrement` functions to modify the private variable `count`.
```js
function createCounter() {
    let count = 0;

    return {
        increment: function() {
            count++;
            console.log(count);
        },
        decrement: function() {
            count--;
            console.log(count);
        }
    };
}

const counter = createCounter();
counter.increment();            // Output: 1
counter.increment();            // Output: 2
counter.decrement();            // Output: 1
```

### Callbacks
Closures are commonly used in **event handlers** or **callbacks**. In this example, the inner function remembers `message` from its outer scope.

```js
function registerClick(message) {
    document.getElementById('submit-button').addEventListener('click', () => {
        console.log(message);
    });
}
```

## Knowledge Check
1. **Basic Behavior**: What will the following code output?
```js
function outer() {
    let outerVariable = 'Hello';
    function inner() {
        console.log(outerVariable);
    }
    return inner;
}

const closure = outer();
closure();
```
<details>
  <summary>Answer</summary>
  The inner function (inner()) forms a closure over the outerVariable defined in the outer() function.   Even though outer() has returned, the closure remembers outerVariable and prints <b>'Hello'</b>.
</details>

2. **Closure with Loops**: What will be the output of the following code, and why? How would you fix it to get the expected result?
```js
for (var i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log(i);
    }, 1000);             // 1000 ms = 1 sec
}
```
<details>
  <summary>Answer</summary>
  <b>3, 3, 3.</b> After 1 second, the for loop has finished and i has been incremented to 3. Since all the setTimeout functions reference the same i, they all print 3. To fix it, print each value of i with a 1-second delay. You can use let since it's block-scoped and each iteration gets its own i. (1) let i = 0. (2) 1000 * i.
</details>
