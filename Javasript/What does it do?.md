

1. What is "new" keyword in Javascript?

The new keyword does the following things: **Creates a blank, plain JavaScript object**. Adds a property to the new object ( __proto__ ) that links to the constructor function's prototype object.

2. What is optional chaining?
Optional chaining is a safe and concise way to perform access checks for nested object properties.

The optional chaining operator `?.` takes the reference to its left and checks if it is undefined or null. If the reference is either of these nullish values, the checks will stop and return undefined. Otherwise, the chain of access checks will continue down the happy path to the final value.

```js
// An empty person object with missing optional location information
const person = {}

// The following will equate to undefined instead of an error
const currentAddress = person.location?.address
```


3.What is Closure?

> A _closure_ is the combination of a function and the lexical environment within which that function was declared.

A closure is an inner function that has access to the outer (enclosing) function’s variables — scope chain. The closure has three scope chains: it has access to its own scope (variables defined between its curly brackets), it has access to the outer function’s variables, and it has access to the global variables.


4. DOM - event.target.value

```js
handleChange(event) {
        this.setState ({
            [event.target.name]: event.target.value
        })
    }
```

 **event.target** - The target event property returns the element that triggered the event. The target property gets the element on which the event originally occurred. So, event.target references DOM element.
 
HTML **name** Attribute - This is a native-html element in browser. The name attribute specifies the name of an element.

The name attribute is used to reference elements in a JavaScript, or to reference form data after a form is submitted.
only-form-elements-with-a-name-attribute-will-have-their-values-passed-when-submitting-a-form)

HTML **value** Attribute - Just like this is a native-html element in browser. As it happens, the DOM node for an element has a ‘value’ property that holds its latest value. I am accessing this from within an handleChange() or onChange() function by e.target.value



4. Undefined?
JavaScript interpreter returns `undefined` when accessing a variable or object property that is not yet initialized.
**Undefined value** primitive value is used when a variable has not been assigned a value.