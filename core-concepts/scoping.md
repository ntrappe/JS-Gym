# Scoping
1. [Global](#global-scope)
2. [Function](#function-scope)
3. [Block](#block-scope)
4. [Knowledge Check](#knowledge-check)

## Global Scope
Variables declared in the **global scope** are accessible from anywhere in the code. 

```js
var husky = 'I am a husky';
let pug = 'I am a pug';
const shiba = 'I am a shiba';

console.log(husky);          // OK, 'I am a husky'
console.log(pug);            // OK, 'I am a pug'
console.log(shiba);          // OK, 'I am a shiba'
```

In a browser environment, globally scoped `var` variables are attached to the `window` object. Other vars—`let` and `const`—**are not** attached to the `window` object.

```js
var husky = 'I am a husky';
let pug = 'I am a pug';
const shiba = 'I am a shiba';

console.log(window.husky);   // OK, 'I am a husky'
console.log(window.pug);     // BAD, 'undefined'
console.log(window.shiba);   // BAD, 'undefined'
```

### Window Object
At the time, global variables were designed to be properties of the **global object**, the `window`. _(In other environments like Node.js, the global object is `global`)_. `Var` was also the only variable at the time. As `let` and `const` were added, people were worried about naming collisions and security risks so they did not allow `let` and `const` to be added to `window` like `var`.

```js
// in browser console, window vars can be queried
window.husky                // 'I am a husky'
```


## Function Scope
Variables declared with `var` are **function-scoped**. They can be accessed anywhere within the function but not outside it.
```js
function hello() {
  var husky = 'I am a husky';
  console.log(husky);        // OK, 'I am a husky'
}
console.log(husky);          // REFERENCE ERROR
```

If you call on a `var` before it's been an initalized, it's **hoisted** to the top of its scope. This just means that you can reference the variable before its actual declaration. So, no error will be thrown. Unlike `var`, `let` and `const` are **not initialized** during hoisting. They are placed in a **temporal dead zone** (TDZ) from the start of the block until the declaration is reached. So you can't access them before they're declared.

This is possible through:
1. Moving the declaration of the `var` variable to the top of its scope during compile.
2. Variable has the value `undefined` until the interpreter reaches the actual assignment.

```js
function hello() {
  console.log(husky);          // 'Undefined'
  var husky = 'I am a husky';
  console.log(husky);          // OK, 'I am a husky'
}
```

```js
function hello() {
  console.log(pug);           // RUNTIME ERROR
  let pug = 'I am a pug';
}
```
### Under the Hood
```js
function hello() {
  var husky;                   // Declaration hoisted to top
  console.log(husky);          // Undefined because of hoisting
  var husky = 'I am a husky';  // Assignment
  console.log(husky);
}
```

## Block Scope
**Block scope** applies to code within `{ }` (e.g. within an `if` statement, loop, or function). Variables `let` and `const` are block-scoped so they are confined to the block in which they are declared.
```js
function hello() {
  let pug = 'I am a pug';
  const shiba = 'I am a shiba';
  console.log(pug);          // OK
  console.log(shiba);        // OK
}
console.log(pug);            // ERROR
console.log(shiba);          // ERROR
```

### Shadowing
If you declare a variable in local scope (function or block) with the same name as a variable in a parent scope, the local one will **shadow** the outer one.
```js
let foo = 'bar';

function hello() {
  let foo = 'win';
  console.log(foo);          // Output: win
}

hello();
console.log(foo);            // Output: bar
```

## Knowledge Check
1. **Declaration & Hoisting**: What will be the following code output and why?
```js
console.log(a); 
var a = 10;
console.log(a); 
```
<details>
  <summary>Answer</summary>
  First, <b>undefined</b> because variable a was hoisted. Then, <b>10</b>.  
</details>

2. **Block Scope**: What will be the result of the following code?
```js
{
    let x = 5;
    const y = 10;
}
console.log(x); 
console.log(y); 
```
<details>
  <summary>Answer</summary>
  Both result in <b>ERROR</b> because x and y are only accessible from inside { }.  
</details>

3. **Function Scope**: Given the following code, what will be the output and why?
```js
function testVarScope() {
    if (true) {
        var a = 20;
    }
    console.log(a); 
}
testVarScope();
```
<details>
  <summary>Answer</summary>
  Output is <b>20</b> because var is function-scoped, so the variable a declared inside the if block is accessible anywhere within the function scope.
</details>

4. **TDZ**: Predict what will happen.
```js
console.log(b);
let b = 15;
```
<details>
  <summary>Answer</summary>
  An <b>ERROR</b> is produced because let is hoisted and stays in the TDZ until initialized.
</details>

5. **Global Scope**: What will be logged to the console and why?
```js
var globalVar = "I'm a var";
let globalLet = "I'm a let";
const globalConst = "I'm a const";

console.log(window.globalVar);   // What will this log?
console.log(window.globalLet);   // What about this?
console.log(window.globalConst); // And this?
```
<details>
  <summary>Answer</summary>
  First, <b>'I'm a var'</b>. Second and third, <b>undefined</b>. Only var can be attached to window object.
</details>
