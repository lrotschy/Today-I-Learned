# How to create closures for classes in ES6

```
// You can pass a class definition to a function as an argument:

function createObject(classDef, name) {
  let n = 1;
  return new classDef(name, (n += 1));
}

let obj = createObject(class {
  sayHi() {
    console.log("hi");
  }
})

obj.sayHi();

// You can immediately invoke an instance of a class:

let dog = new class {
  constructor(name) {
    this.name = name;
  }

  sayName() {
    console.log(this.name);
  }
}("Ruby");

dog.sayName();

// You can also create a closure with an IIFE so that 
// you can keep class information that updates with every new instance.

class Person {
  constructor(name, n = 0) {
    this.name = name;
    this.number = n;
  }
}

let counter = (function () {
  let n = 1;
  return function (classDef, name) {
    n += 1;
    return new classDef(name, n);
  }
})();

let me = counter(Person, "liela");
console.log(me.number) // 1
let ruby = counter(Person, "ruby");
console.log(ruby.number) // 2
let michael = counter(Person, "michael");
console.log(michael.number) // 3

```
