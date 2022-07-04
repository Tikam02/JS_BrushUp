## Var and Const 

**The const Keyword

A constant is a variable that cannot be overwritten. Once declared, you cannot
change its value. A lot of the variables that we create in JavaScript should not be over‐
written, so we’ll be using const a lot. Like other languages had done before it, Java‐
Script introduced constants with ES6.
Before constants, all we had were variables, and variables could be overwritten:

var pizza = true;
pizza = false;
console.log(pizza); // false

We cannot reset the value of a constant variable, and it will generate a console error
(as shown in Figure 2-1) if we try to overwrite the value:

const pizza = true;
pizza = false;

**The let Keyword

JavaScript now has lexical variable scope. In JavaScript, we create code blocks with
curly braces ( {} ). In functions, these curly braces block off the scope of any variable
declared with var . On the other hand, consider if/else statements. If you’re coming
from other languages, you might assume that these blocks would also block variable
scope. This was not the case until let came along.
If a variable is created inside of an if/else block, that variable is not scoped to the
block:
```js
var topic = "JavaScript";
if (topic) {
var topic = "React";
console.log("block", topic); // block React
}
console.log("global", topic); // global React
```

The topic variable inside the if block resets the value of topic outside of the block.
With the let keyword, we can scope a variable to any code block. Using let protects
the value of the global variable:

```js
var topic = "JavaScript";
if (topic) {
let topic = "React";
console.log("block", topic); // React
}
console.log("global", topic); // JavaScript
```



## Template Strings
Template strings provide us with an alternative to string concatenation. They also
allow us to insert variables into a string. You’ll hear these referred to as template
strings, template literals, or string templates interchangeably.
Traditional string concatenation uses plus signs to compose a string using variable
values and strings:

```js

console.log(lastName + ", " + firstName + " " + middleName);
```

With a template, we can create one string and insert the variable values by surround‐
ing them with ${ } :

```js
console.log(`${lastName}, ${firstName} ${middleName}`);
```

Any JavaScript that returns a value can be added to a template string between the
${ } in a template string.



## Functions


Function Declarations
A function declaration or function definition starts with the function keyword,
which is followed by the name of the function, logCompliment . The JavaScript state‐
ments that are part of the function are defined between the curly braces:

```js
function logCompliment() {
console.log("You're doing great!");
}
```
Once you’ve declared the function, you’ll invoke or call it to see it execute:
```js
function logCompliment() {
console.log("You're doing great!");
}
logCompliment();
```

Once invoked, you’ll see the compliment logged to the console.

Function Expressions
Another option is to use a function expression. This just involves creating the func‐
tion as a variable:
```js
const logCompliment = function() {
console.log("You're doing great!");
};
logCompliment();
```
The result is the same, and You're doing great! is logged to the console.
One thing to be aware of when deciding between a function declaration and a func‐
tion expression is that function declarations are hoisted and function expressions are
not.

In other words, you can invoke a function before you write a function declara‐tion. You cannot invoke a function created by a function expression. This will cause
an error. For example:
```js
// Invoking the function before it's declared
hey();
// Function Declaration
function hey() {
alert("hey!");
}
```
This works. You’ll see the alert appear in the browser. It works because the function is
hoisted, or moved up, to the top of the file’s scope. Trying the same exercise with a
function expression will cause an error:
```js
// Invoking the function before it's declared
hey();
// Function Expression
const hey = function() {
alert("hey!");
};
```
TypeError: hey is not a function
This is obviously a small example, but this TypeError can occasionally arise when
importing files and functions in a project. If you see it, you can always refactor as a
declaration.

### Passing arguments
The logCompliment function currently takes in no arguments or parameters. If we
want to provide dynamic variables to the function, we can pass named parameters to
a function simply by adding them to the parentheses. Let’s start by adding a first
Name variable:
```js
const logCompliment = function(firstName) {
console.log(`You're doing great, ${firstName}`);
};
logCompliment("Molly");
```
Now when we call the logCompliment function, the firstName value sent will be
added to the console message.
We could add to this a bit by creating another argument called message . Now, we
won’t hard-code the message. We’ll pass in a dynamic value as a parameter:
```js
const logCompliment = function(firstName, message) {
console.log(`${firstName}: ${message}`);
};
logCompliment("Molly", "You're so cool");
```

## Arrow Functions
Arrow functions are a useful new feature of ES6. With arrow functions, you can cre‐
ate functions without using the function keyword.

```js
const lordify = function(firstName) {
return `${firstName} of Canterbury`;
};
console.log(lordify("Dale")); // Dale of Canterbury
console.log(lordify("Gail")); // Gail of Canterbury
```

With an arrow function, we can simplify the syntax tremendously:

```js
const lordify = firstName => `${firstName} of Canterbury`;
```

With the arrow, we now have an entire function declaration on one line. The func
tion keyword is removed. We also remove return because the arrow points to what
should be returned. Another benefit is that if the function only takes one argument,
we can remove the parentheses around the arguments

More than one argument should be surrounded by parentheses:

```js
// Typical function
const lordify = function(firstName, land) {
return `${firstName} of ${land}`;
};
// Arrow Function
const lordify = (firstName, land) => `${firstName} of ${land}`;
console.log(lordify("Don", "Piscataway")); // Don of Piscataway
console.log(lordify("Todd", "Schenectady")); // Todd of Schenectady
```



### Returning objects
What happens if you want to return an object? Consider a function called person that
builds an object based on parameters passed in for firstName and lastName :
```js
const person = (firstName, lastName) =>
{
first: firstName,
last: lastName
}
console.log(person("Brad", "Janson"));
```
As soon as you run this, you’ll see the error: Uncaught SyntaxError: Unexpected
token : . To fix this, just wrap the object you’re returning with parentheses:
```js
const person = (firstName, lastName) => ({
first: firstName,
last: lastName
});

console.log(person("Flad", "Hanson"));
```

These missing parentheses are the source of countless bugs in JavaScript and React
apps, so it’s important to remember this one!



## Destructing Objects:

Destructuring Objects
Destructuring assignment allows you to locally scope fields within an object and to
declare which values will be used. Consider the sandwich object. It has four keys, but
we only want to use the values of two. We can scope bread and meat to be used
locally:
```js
const sandwich = {
	bread: "dutch crunch",
	meat: "tuna",
	cheese: "swiss",
	toppings: ["lettuce", "tomato", "mustard"]
};
const { bread, meat } = sandwich;
console.log(bread, meat); // dutch crunch tuna
```
The code pulls bread and meat out of the object and creates local variables for them.
Also, since we declared these destructed variables using let , the bread and meat vari‐
ables can be changed without changing the original sandwich:

```js
const sandwich = {
	bread: "dutch crunch",
	meat: "tuna",
	cheese: "swiss",
	toppings: ["lettuce", "tomato", "mustard"]
};
let { bread, meat } = sandwich;
	bread = "garlic";
	meat = "turkey";
	
console.log(bread); // garlic
console.log(meat); // turkey
console.log(sandwich.bread, sandwich.meat); // dutch crunch tuna
```
We can also destructure incoming function arguments. Consider this function that
would log a person’s name as a lord:
```js
const lordify = regularPerson => {
	console.log(`${regularPerson.firstname} of Canterbury`);
};

const regularPerson = {
	firstname: "Bill",
	lastname: "Wilson"
};
lordify(regularPerson); // Bill of Canterbury
```

Instead of using dot notation syntax to dig into objects, we can destructure the values
we need out of regularPerson :
```js
const lordify = ({ firstname }) => {
	console.log(`${firstname} of Canterbury`);
};
const regularPerson = {
	firstname: "Bill",
	lastname: "Wilson"
};
lordify(regularPerson); // Bill of Canterbury
```
Let’s take this one level farther to reflect a data change. Now, the regularPerson
object has a new nested object on the spouse key:
```js
const regularPerson = {
	firstname: "Bill",
	lastname: "Wilson",
		spouse: {
			firstname: "Phil",
			lastname: "Wilson"
		}
};
```
If we wanted to lordify the spouse’s first name, we’d adjust the function’s destructured
arguments slightly:
```js
const lordify = ({ spouse: { firstname } }) => {
	console.log(`${firstname} of Canterbury`);
};
lordify(regularPerson); // Phil of Canterbury
```

Using the colon and nested curly braces, we can destructure the firstname from the
spouse object.


### Object Literal Enhancement
Object literal enhancement is the opposite of destructuring. It’s the process of restruc‐
turing or putting the object back together. With object literal enhancement, we can
grab variables from the global scope and add them to an object:
```js
const name = "Tallac";
const elevation = 9738;
const funHike = { name, elevation };
console.log(funHike); // {name: "Tallac", elevation: 9738}
```
name and elevation are now keys of the funHike object.

### The Spread Operator
The spread operator is three dots ( ... ) that perform several different tasks. First, the
spread operator allows us to combine the contents of arrays. For example, if we had
two arrays, we could make a third array that combines the two arrays into one:

```js
const peaks = ["Tallac", "Ralston", "Rose"];
const canyons = ["Ward", "Blackwood"];
const tahoe = [...peaks, ...canyons];
console.log(tahoe.join(", ")); // Tallac, Ralston, Rose, Ward, Blackwood
```

Let’s take a look at how the spread operator can help us deal with a problem. Using
the peaks array from the previous sample, let’s imagine that we wanted to grab the
last item from the array rather than the first. We could use the Array.reverse
method to reverse the array in combination with array destructuring:

```js
const peaks = ["Tallac", "Ralston", "Rose"];
const [last] = peaks.reverse();
console.log(last); // Rose
console.log(peaks.join(", ")); // Rose, Ralston, Tallac
```

See what happened? The reverse function has actually altered or mutated the array.
In a world with the spread operator, we don’t have to mutate the original array.
Instead, we can create a copy of the array and then reverse it:

```js
const peaks = ["Tallac", "Ralston", "Rose"];
const [last] = [...peaks].reverse();
console.log(last); // Rose
console.log(peaks.join(", ")); // Tallac, Ralston, Rose
```

Since we used the spread operator to copy the array, the peaks array is still intact and
can be used later in its original form.

The spread operator can also be used to get the remaining items in the array:
```js
const lakes = ["Donner", "Marlette", "Fallen Leaf", "Cascade"];
const [first, ...others] = lakes;
console.log(others.join(", ")); // Marlette, Fallen Leaf, Cascade
```

We can also use the three-dot syntax to collect function arguments as an array. When
used in a function, these are called rest parameters . Here, we build a function that
takes in n number of arguments using the spread operator, then uses those arguments
to print some console messages:


```js
function directions(...args) {
	let [start, ...remaining] = args;
	let [finish, ...stops] = remaining.reverse();
	console.log(`drive through ${args.length} towns`);
	console.log(`start in ${start}`);
	console.log(`the destination is ${finish}`);
	console.log(`stopping ${stops.length} times in between`);
}
directions("Truckee", "Tahoe City", "Sunnyside", "Homewood", "Tahoma");
```


Using the spread operator with objects is similar to using it with
arrays. In this example, we’ll use it the same way we combined two arrays into a third
array, but instead of arrays, we’ll use objects:

```js
const morning = {

breakfast: "oatmeal",

lunch: "peanut butter and jelly"

};

const dinner = "mac and cheese";

const backpackingMeals = {

...morning,

dinner

};

console.log(backpackingMeals);
```

Response:

```js
1.  {breakfast: "oatmeal", lunch: "peanut butter and jelly", dinner: "mac and cheese"}
    
    1.   breakfast: "oatmeal"
        
    2.   lunch: "peanut butter and jelly"
        
    3.   dinner: "mac and cheese"
```


## Asynchronous Function

The then method will invoke the callback function once the promise has resolved.
Whatever you return from this function becomes the argument of the next then
function. So we can chain together then functions to handle a promise that has been
successfully resolved:
```js
fetch("https://api.randomuser.me/?nat=US&results=1")
	.then(res => res.json())
	.then(json => json.results)
	.then(console.log)
	.catch(console.error);
```

First, we use fetch to make a GET request to randomuser.me. If the request is suc‐
cessful, we’ll then convert the response body to JSON. Next, we’ll take the JSON data
and return the results, then we’ll send the results to the console.log function, which
will log them to the console. Finally, there is a catch function that invokes a callback
if the fetch did not resolve successfully. Any error that occurred while fetching data
from randomuser.me will be based on that callback. Here, we simply log the error to
the console using console.error


### Async/Await
Another popular approach for handling promises is to create an async function.
Some developers prefer the syntax of async functions because it looks more familiar,
like code that’s found in a synchronous function. Instead of waiting for the results of
a promise to resolve and handling it with a chain of then functions, async functions
can be told to wait for the promise to resolve before further executing any code found
in the function.

```js
const getFakePerson = async () => {
let res = await fetch("https://api.randomuser.me/?nat=US&results=1");
let { results } = res.json();
console.log(results);
};
getFakePerson();
```

Notice that the getFakePerson function is declared using the async keyword. This
makes it an asynchronous function that can wait for promises to resolve before exe‐
cuting the code any further. The await keyword is used before promise calls. This
tells the function to wait for the promise to resolve. This code accomplishes the exact
same task as the code in the previous section that uses then functions. Well, almost
the exact same task…
```js
const getFakePerson = async () => {
	try {
		let res = await fetch("https://api.randomuser.me/?nat=US&results=1");
		let { results } = res.json();
		console.log(results);
	}catch (error) {
		console.error(error);
	}
};
getFakePerson();
```


### Building Promises


The getPeople function returns a new promise. The promise makes a request to the
API. If the promise is successful, the data will load. If the promise is unsuccessful, an
error will occur:
```js
const getPeople = count =>
	new Promise((resolves, rejects) => {
	const api = `https://api.randomuser.me/?nat=US&results=${count}`;
	const request = new XMLHttpRequest();
	request.open("GET", api);
		request.onload = () =>
		request.status === 200
			? resolves(JSON.parse(request.response).results)
			: reject(Error(request.statusText));
	request.onerror = err => rejects(err);
	request.send();
});
```
With that, the promise has been created, but it hasn’t been used yet. We can use the
promise by calling the getPeople function and passing in the number of members
that should be loaded. The then function can be chained on to do something once the
promise has been fulfilled. When a promise is rejected, any details are passed back to
the catch function, or the catch block if using async/await syntax:

```js
getPeople(5)
.then(members => console.log(members))
.catch(error => console.error(`getPeople failed: ${error.message}`))
);
```

