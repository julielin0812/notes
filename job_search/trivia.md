# Trivia Questions

## JavaScript

### What is the difference between a variable that is null, undefined, or undeclared?
- Undeclared variable hasn't been declared yet.
- Undefined variable has been declared but has not had a value assigned to it. (ex. `let a;`)
- `null` variable is a declared variable with the value of `null` assigned to it.

Source: [Frontend Interview Questions - The Basics](https://github.com/rlee0525/TechnicalConceptsForInterviews/blob/master/FrontendBasics.md#whats-the-difference-between-a-variable-that-is-null-undefined-or-undeclared)

### What is the difference between `==` and `===`
"... `==` will not check types and `===` will check whether both sides are of same type. So, `==` is tolerant. But under the hood it converts to its convenient type to have both in same type and then do the comparison.

`===` compares the types and values. Hence, if both sides are not same type, answer is always false. For example, if you are comparing two strings, they must have identical character sets. For other primitives (number, boolean) must share the same value.

Rule for implicit coercion: Comparison by using `==` does implicit type conversion under the hood. And rules for implicit coercion are as follows-

If both operands are same type use `===`
undefined `==` null
If one operands is string another is number, convert string to number
If one is boolean and another is non-boolean, convert boolean to number and then perform comparison
While comparing a string or number to an object, try to convert the object to a primitive type and then try to compare
Be careful while comparing objects, identifiers must reference the same objects or same array.

**Special note**: `NaN`, `null` and `undefined` will never `===` another type. `NaN` does not even `===` itself."

Source: [thatjsdude.com - JS: Basics and Tricky Questions](http://www.thatjsdude.com/interview/js2.html#doubleVsTripleEqual)

### Explain the difference between classical inheritance and prototypal inheritance.

The great thing about JavaScript is the ability to do away with the rigid rules of classical inheritance and let objects inherit properties from other objects.

**Classical Inheritance**: A constructor function instantiates an instance via the “new” keyword. This new instance inherits properties from a parent class.

**Prototypal Inheritance**: An instance is created by cloning an existing object that serves as a prototype. This instance—often instantiated using a factory function or “Object.create()”—can benefit from selective inheritance from many different objects.

Source: [15 JavaScript interview questions and answers](https://www.upwork.com/i/interview-questions/javascript/)

### What are prototypes in JavaScript?

"Prototypes are the mechanism by which JavaScript objects inherit features from one another, and they work differently than inheritance mechanisms in classical object-oriented programming languages."

"JavaScript is often described as a **prototype-based language** — each object has a **prototype object**, which acts as a template object that it inherits methods and properties from. An object's prototype object may also have a prototype object, which it inherits methods and properties from, and so on. This is often referred to as a **prototype chain**, and explains why different objects have properties and methods defined on other objects available to them.

Well, to be exact, the properties and methods are defined on the `prototype` property on the Objects' constructor functions, not the object instances themselves."

"...a link is made between the object instance and its prototype (its `__proto__` property, which is derived from the `prototype` property on the constructor), and the properties and methods are found by walking up the chain of prototypes."

Source: [Object Prototypes MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)


### Explain the difference between pass by value and pass by reference.
Primitive type (`null`, `undefined` , `boolean`, `number`, `string` and ES6 `symbol`) are passed by value and objects are passed by reference. If you change a property of the passed object, the change will be affected. However, you assign a new object to the passed object, the changes will not be reflected.

Example:
```JavaScript
var a = 2;        // 'a' hold a copy of the value 2.
var b = a;        // 'b' is always a copy of the value in 'a'
b++;
console.log(a);   // 2
console.log(b);   // 3
var c = [1,2,3];
var d = c;        // 'd' is a reference to the shared value
d.push( 4 );      // Mutates the referenced value (object)
console.log(c);   // [1,2,3,4]
console.log(d);   // [1,2,3,4]
/* Compound values are equal by reference */
var e = [1,2,3,4];
console.log(c === d);  // true
console.log(c === e);  // false
```

Sources:
- [That JS Dude | Pass by value vs by reference](https://thatjsdude.com/interview/js2.html#byValueByRef)
- [freecodecamp | The Definitive JavaScript Handbook for a developer interview](https://medium.freecodecamp.org/the-definitive-javascript-handbook-for-a-developer-interview-44ffc6aeb54e)


### What is the drawback of creating a true private function in JS?
"One of the drawbacks of creating true private methods in JavaScript is that they are very memory-inefficient, as a new copy of the method would be created for each instance."

```JavaScript
var Employee = function (name, company, salary) {
    this.name = name || "";       //Public attribute default value is null
    this.company = company || ""; //Public attribute default value is null
    this.salary = salary || 5000; //Public attribute default value is null

    // Private method
    var increaseSalary = function () {
        this.salary = this.salary + 1000;
    };

    // Public method
    this.dispalyIncreasedSalary = function() {
        increaseSlary();
        console.log(this.salary);
    };
};

// Create Employee class object
var emp1 = new Employee("John","Pluto",3000);
// Create Employee class object
var emp2 = new Employee("Merry","Pluto",2000);
// Create Employee class object
var emp3 = new Employee("Ren","Pluto",2500);
```
"Here each instance variable `emp1`, `emp2`, `emp3` has its own copy of the increaseSalary private method.

So, as a recommendation, don’t use private methods unless it’s necessary."

Source: [CodeMentor | 21 Essential JavaScript Interview Questions](https://www.codementor.io/nihantanu/21-essential-javascript-tech-interview-practice-questions-answers-du107p62z#what-is-the-drawback-of-creating-true-private-methods-in-javascript)

### Explain the difference between `Function`, `Method` and `Constructor` calls in JavaScript.
"In JavaScript, these are just three different usage patterns of one single construct.

functions : The simplest usages of function call:
```JavaScript
function helloWorld(name) {
  return "hello world, " + name;
}

helloWorld("JS Geeks"); // "hello world JS Geeks"
```
Methods in JavaScript are nothing more than object properties that reference to a function.
```JavaScript
var obj = {
  helloWorld : function() {
    return "hello world, " + this.name;
  },
  name: 'John Carter'
}

obj.helloWorld(); // // "hello world John Carter"
```
Notice how `helloWorld` refer to `this` properties of obj. Here it's clear or you might have already understood that `this` gets bound to `obj`. But the interesting point that we can copy a reference to the same function `helloWorld` in another object and get a difference answer. Let see:
```JavaScript
var obj2 = {
  helloWorld : obj.helloWorld,
  name: 'John Doe'
}
obj2.helloWorld(); // "hello world John Doe"
```
You might be wondering what exactly happens in a method call here. Here we call the expression itself determine the binding of this `this`, The expression `obj2.helloWorld()` looks up the helloWorld property of obj and calls it with receiver object `obj2`.

The third use of functions is as constructors. Like function and method, constructors are defined with function.
```JavaScript
function Employee(name, age) {
  this.name = name;
  this.age = age;
}

var emp1 = new Employee('John Doe', 28);
emp1.name; // "John Doe"
emp1.age; // 28
```
Unlike function calls and method calls, a constructor call `new Employee('John Doe', 28)` create a brand new object and passes it as the value of `this`, and implicitly returns the new object as its result.

The primary role of the constructor function is to initialize the object."

Source: [123 Essential JavaScript Interview Questions](https://github.com/nishant8BITS/123-Essential-JavaScript-Interview-Question#difference-between-function-method-and-constructor-calls-in-javascript)