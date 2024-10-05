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
