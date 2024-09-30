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
