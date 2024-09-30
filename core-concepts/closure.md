# Closure
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
