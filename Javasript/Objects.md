
# Objects


- Objects :
	- JS object declartion
	- Object Properties
	- Accessing Objects
	- Methods
	- Constructor Functions
	- Prototypes
	- Classes
	- Getters, setters, and statics
	- Inheritence





### Object Declaration
```
const object_name = {
   key1: value1,
   key2: value2
}
```

example:
```js
// object creation
const person = { 
    name: 'John',
    age: 20
};
console.log(typeof person); // object
```

OR
```js
const person = { name: 'John', age: 20 };
```


### Object Properties

In JavaScript, "key: value" pairs are called **properties**

`name: 'John'` and `age: 20` are properties.


### Accessing Object Properties

1.Using dot Notation

Syntax -   objectName.key

```js
const person = { 
    name: 'John', 
    age: 20, 
};

// accessing property
console.log(person.name); // John
```


2.Using bracket Notation

Syntax - ```objectName["propertyName"]```

```js
const person = { 
    name: 'John', 
    age: 20, 
};

// accessing property
console.log(person["name"]); // John
```

3. Accessing Nested Objects 
```js
// nested object
const student = { 
    name: 'John', 
    age: 20,
    marks: {
        science: 70,
        math: 75
    }
}

// accessing property of student object
console.log(student.marks); // {science: 70, math: 75}

// accessing property of marks object
console.log(student.marks.science); // 70
```

### Methods
> the JavaScript **method** is an object property that has a function value.

Methods are nothing more than properties that hold function values.

```js
// object containing method
const person = {
    name: 'John',
    greet: function() { console.log('hello'); }
};
```

You can access an object method using a dot notation. The syntax is:

```
objectName.methodKey()
```


```js
// accessing method and property
const person = {
    name: 'John',
    greet: function() { console.log('hello'); }
};

// accessing property
person.name; // John

// accessing method
person.greet(); // hello
```


**Adding a Method to a JavaScript Object

```js

// creating an object
let student = { };

// adding a property
student.name = 'John';

// adding a method
student.greet = function() {
    console.log('hello');
}

// accessing a method
student.greet(); // hello
```


To access a property of an object from within a method of the same object, you need to use the `this` keyword.

```js
const person = {
    name: 'John',
    age: 30,

    // accessing name property by using this.name
    greet: function() { console.log('The name is' + ' ' + this.name); }
};

person.greet();
```



### Constructor function
In JavaScript, a constructor function is used to create objects.

```js
// constructor function
function Person () {
    this.name = 'John',
    this.age = 23
}

// create an object
const person = new Person();
```


In JavaScript, when `this` keyword is used in a constructor function, `this` refers to the object when the object is created.
```js
// constructor function
function Person () {
    this.name = 'John',
}

// create object
const person1 = new Person();

// access properties
console.log(person1.name);  // John
```


#### JavaScript Constructor Function Parameters

```js
// constructor function
function Person (person_name, person_age, person_gender) {

   // assigning  parameter values to the calling object
    this.name = person_name,
    this.age = person_age,
    this.gender = person_gender,

    this.greet = function () {
        return ('Hi' + ' ' + this.name);
    }
}


// creating objects
const person1 = new Person('John', 23, 'male');
const person2 = new Person('Sam', 25, 'female');

// accessing properties
console.log(person1.name); // "John"
console.log(person2.name); // "Sam"

```




#### Adding Properties And Methods in an Object

You can add properties or methods in an object like this:

If you put the keyword `new` in front of a function call, the function is treated as a constructor. This means that an object with the right prototype is automatically created, bound to `this` in the function, and returned at the end of the function.

The prototype object used when constructing objects is found by taking the `prototype` property of the constructor function.

```js
// constructor function
function Person () {
    this.name = 'John',
    this.age = 23
}

// creating objects
let person1 = new Person();
let person2 = new Person();

// adding property to person1 object
person1.gender = 'male';

// adding method to person1 object
person1.greet = function () {
    console.log('hello');
}

person1.greet();   // hello

// Error code
// person2 doesn't have greet() method
person2.greet();
```



**Output

```js
hello
Uncaught TypeError: person2.greet is not a function
```


### What is the Prototype in JavaScript?
#### Adding Properties And Methods in an Object using prototype


A prototype is an inbuilt object where it associated with the functions by default, which can be accessible, modifiable, and create new variables and methods to it and share across all the instances of its constructor function.


```js
// constructor function
function Person () {
    this.name = 'John',
    this.age = 23
}

// creating objects
let person1 = new Person();
let person2 = new Person();

// adding new property to constructor function
Person.prototype.gender = 'Male';

console.log(person1.gender); // Male
console.log(person2.gender); // Male
```


#### Prototype Inheritance

In JavaScript, a prototype can be used to add properties and methods to a constructor function. And objects inherit properties and methods from a prototype. For example,


```js
// constructor function
function Person () {
    this.name = 'John',
    this.age = 23
}

// creating objects
const person1 = new Person();
const person2 = new Person();

// adding property to constructor function
Person.prototype.gender = 'male';

// prototype value of Person
console.log(Person.prototype);

// inheriting the property from prototype
console.log(person1.gender);
console.log(person2.gender);
```

**output

```js
{ gender: "male" }
male
male
```

#### Add Methods to a Constructor Function Using Prototype


You can also add new methods to a constructor function using prototype. For example,


```js
// constructor function
function Person () {
    this.name = 'John',
    this.age = 23
}

// creating objects
const person1 = new Person();
const person2 = new Person();

// adding a method to the constructor function
Person.prototype.greet = function() {
    console.log('hello' + ' ' +  this.name);
}

person1.greet(); // hello John
person2.greet(); // hello John
```



#### Changing Prototype

If a prototype value is changed, then all the new objects will have the changed property value. All the previously created objects will have the previous value. For example,

```js
// constructor function
function Person() {
    this.name = 'John'
}

// add a property
Person.prototype.age = 20;

// creating an object
const person1 = new Person();

console.log(person1.age); // 20

// changing the property value of prototype
Person.prototype = { age: 50 }

// creating new object
const person3 = new Person();

console.log(person3.age); // 50
console.log(person1.age); // 20
```



### Classes

 A class defines the shape of a type of object—what methods and properties it has. Such an object is called an _instance_ of the class.
 
A class is a blueprint for the object. You can create an object from the class.

You can think of the class as a sketch (prototype) of a house. It contains all the details about the floors, doors, windows, etc. Based on these descriptions, you build the house. House is the object.

The `class` keyword starts a class declaration, which allows us to define a constructor and a set of methods all in a single place. Any number of methods may be written inside the declaration’s braces. The one named `constructor` is treated specially. It provides the actual constructor function.

Creating a class 

A constructor is a special function that creates and initializes an object instance of a class. In JavaScript, a constructor gets called when an object is created using the **new keyword**. The purpose of a constructor is to create a new object and set values for any existing object propertie


without using class keyword and creating a constructor function:

```js
// constructor function
function Person () {
    this.name = 'John',
    this.age = 23
}
// create an object
const person1 = new Person();
```

Using Class Keyword creating constructor function:

```js
// creating a class
class Person {
  constructor(name) {
    this.name = name;
  }
}
```

The `class` keyword is used to create a class. The properties are assigned in a constructor function.

Create object :


```js
// creating a class
class Person {
  constructor(name) {
    this.name = name;
  }
}

// creating an object
const person1 = new Person('John');
const person2 = new Person('Jack');

console.log(person1.name); // John
console.log(person2.name); // Jack
```

**Class Methods

While using constructor function, you define methods as:

```js
// constructor function
function Person (name) {

   // assigning  parameter values to the calling object
    this.name = name;

    // defining method
    this.greet = function () {
        return ('Hello' + ' ' + this.name);
    }
}
```

greet is method.


```js
class Person {
    constructor(name) {
    this.name = name;
  }

    // defining method
    greet() {
        console.log(`Hello ${this.name}`);
    }
}

let person1 = new Person('John');

// accessing property
console.log(person1.name); // John

// accessing method
person1.greet(); // Hello John
```


**Setters and Getters

Interfaces often consist mostly of methods, but it is also okay to include properties that hold non-function values. For example, `Map` objects have a `size` property that tells you how many keys are stored in them.

It is not even necessary for such an object to compute and store such a property directly in the instance. Even properties that are accessed directly may hide a method call. Such methods are called _getters_, and they are defined by writing `get` in front of the method name in an object expression or class declaration.

getter

The **`get`** syntax binds an object property to a function that will be called when that property is looked up.

```js
const obj = {
  log: ['a', 'b', 'c'],
  get latest() {
    if (this.log.length === 0) {
      return undefined;
    }
    return this.log[this.log.length -1];
  }
};

console.log(obj.latest);
// expected output: "c"
```


The **`set`** syntax binds an object property to a function to be called when there is an attempt to set that property.

```js
const language = {
  set current(name) {
    this.log.push(name);
  },
  log: []
};

language.current = 'EN';
language.current = 'FA';

console.log(language.log);
// expected output: Array ["EN", "FA"]
```




**Class Inheritance


To use class inheritance, you use the `extends` keyword. For example,


```js
// parent class
class Person { 
    constructor(name) {
        this.name = name;
    }

    greet() {
        console.log(`Hello ${this.name}`);
    }
}

// inheriting parent class
class Student extends Person {

}

let student1 = new Student('Jack');
student1.greet();
```

ouput:
```
Hello Jack
```


**JavaScript super() keyword

The `super` keyword used inside a child class denotes its parent class.

```js
// parent class
class Person { 
    constructor(name) {
        this.name = name;
    }
    greet() {
        console.log(`Hello ${this.name}`);
    }
}

// inheriting parent class
class Student extends Person {
    constructor(name) {
        console.log("Creating student class");
        // call the super class constructor and pass in the name parameter
        super(name);
    }
}

let student1 = new Student('Jack');
student1.greet();
```


***Overriding Method or Property

If a child class has the same method or property name as that of the parent class, it will use the method and property of the child class. This concept is called method overriding.


```js
// parent class
class Person { 
    constructor(name) {
        this.name = name;
        this.occupation = "unemployed";
    }
    greet() {
        console.log(`Hello ${this.name}.`);
    }
}

// inheriting parent class
class Student extends Person {
    constructor(name) {
        // call the super class constructor and pass in the name parameter
        super(name);
        // Overriding an occupation property
        this.occupation = 'Student';
    }
    
    // overriding Person's method
    greet() {
        console.log(`Hello student ${this.name}.`);
        console.log('occupation: ' + this.occupation);
    }
}

let p = new Student('Jack');
p.greet();
```




-------------------------------------------------------

Refs:

https://www.toolsqa.com/javascript/prototype-in-javascript/
https://dev.to/lydiahallie/javascript-visualized-scope-chain-13pd