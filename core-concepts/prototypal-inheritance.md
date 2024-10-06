# Prototypal Inheritance

1. [Definition](#definition)

## Definition
**Prototypal inheritance** is the mechanism by which objects can inherit properties and methods
from other objects. Unlike classical inheritance (like in C++), where classes inherit from other classes, 
JavaScript objects inherit _directly_ from other objects.

At the heart of this mechanism is the **prototype chain** which is a series of objects
connected via their `__proto__` or `prototype` property. When you try to access a property
or method on an object, JS first looks for it on the object itself. If not found, it climbs
the chain to find it.

### Basic Example
```js
const person = {
  name: 'John',
  greet: function() { console.log(`Hi, I'm ${this.name}`); }
};

const student = {
  __proto__: person,    // student inherits from person
  school: 'UCSD',
};

console.log(student.name);    // Output: John. Inherited from person
student.greet();              // Output: Hi, I'm John.
```

## Constructor Functions
Constructor functions allow you to create multiple instances of an object that share
properties and methods. Each function has a special `protoype` property which is an 
object that will be inherited by any object created using that function as a constructor.

### Instance of Person Object
```js
function Person(name) {
  this.name = name;
}

const chiasa = new Person('Chiasa);
```

### Calling Method Not Found in Prototype Chain
```js
function Person(name) {
  this.name = name;
}

const chiasa = new Person('Chiasa);
chiasa.greet();        // not defined => TypeError
```

### Calling Method Found
```js
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hi, I'm ${this.name}`);
};

const chiasa = new Person('Chiasa);
chiasa.greet();      // Output: Hi, I'm Chiasa
```

## Prototype Chain
When you try to access a property, JS first checks if that objct has it. If not, it keeps
going up the `__proto__` link to look for it until it hits `null`.

### Direct Prototype Manipulation (Explicit)
Assigning `__proto__` directly is not the standard approach. It makes the prototype chain more
clear when learning but it's less formal and less safe in production.

```js
const dog = {
  food: 'kibble'
};

const spitz = {
  __proto__: dog,
  weather: 'cold'
};

const samoyed = {
  __proto__: spitz,
  color: 'white'
};

console.log(samoyed.color);        // white
console.log(samoyed.weather);      // cold
console.log(samoyed.food);         // kibble
```

### Constructor Functions (Implicit)
The more traditional approach is to establish inheritance through constructor functions and setting
the prototype via `Object.create()`.

```js
function Dog() = {
  this.food = 'kibble';
}

function Spitz() {
  Dog.call(this);      // Call parent constructor to inherit parent properties
  this.weather = 'cold';
}

// Spitz inherits from Dog
Spitz.prototype = Object.create(Dog.prototype);
Spitz.prototype.constructor = Spitz;    // Reset constructor reference

function Samoyed() {
  Spitz.call(this);
  this.color = 'white';
}

// Samoyed inherits from Spitz
Samoyed.prototype = Object.create(Spitz.prototype);
Samoyed.prototype.constructor = Samoyed;

// New instance of samoyed
const sammy = new Samoyed();

console.log(sammy.color);      // white
console.log(sammy.weather);    // cold
```

