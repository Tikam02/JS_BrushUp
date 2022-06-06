

As seen in the previous challenge, `const` declaration alone doesn't really protect your data from mutation. To ensure your data doesn't change, JavaScript provides a function `Object.freeze` to prevent data mutation.




#### Use Arrow Functions to Write Concise Anonymous Functions

In JavaScript, we often don't need to name our functions, especially when passing a function as an argument to another function. Instead, we create inline functions. We don't need to name these functions because we do not reuse them anywhere els

```js
const myFunc = function() {
  const myVar = "value";
  return myVar;
}
```

ES6 provides us with the syntactic sugar to not have to write anonymous functions this way. Instead, you can use **arrow function syntax**:

```js
const myFunc = () => {
  const myVar = "value";
  return myVar;
}
```


Just like a regular function, you can pass arguments into an arrow function.

```js
const doubler = (item) => item * 2;
doubler(4);
```

In order to help us create more flexible functions, ES6 introduces default parameters for functions.

Check out this code:

```js
const greeting = (name = "Anonymous") => "Hello " + name;

console.log(greeting("John"));
console.log(greeting());
```

The console will display the strings `Hello John` and `Hello Anonymous`.

The default parameter kicks in when the argument is not specified (it is undefined). As you can see in the example above, the parameter `name` will receive its default value `Anonymous` when you do not provide a value for the parameter. You can add default values for as many parameters as you want.

#### Use the Rest Parameter with Function Parameters

In order to help us create more flexible functions, ES6 introduces the rest parameter for function parameters. With the rest parameter, you can create functions that take a variable number of arguments. These arguments are stored in an array that can be accessed later from inside the function.

Check out this code:

```js
function howMany(...args) {
  return "You have passed " + args.length + " arguments.";
}
console.log(howMany(0, 1, 2));
console.log(howMany("string", null, [1, 2, 3], { }));
```

The console would display the strings `You have passed 3 arguments.` and `You have passed 4 arguments.`.

The rest parameter eliminates the need to check the `args` array and allows us to apply `map()`, `filter()` and `reduce()` on the parameters array

#### Use the Spread Operator to Evaluate Arrays In-Place

ES6 introduces the spread operator, which allows us to expand arrays and other expressions in places where multiple parameters or elements are expected.

The ES5 code below uses `apply()` to compute the maximum value in an array:

```js
var arr = [6, 89, 3, 45];
var maximus = Math.max.apply(null, arr);
```

`maximus` would have a value of `89`.

We had to use `Math.max.apply(null, arr)` because `Math.max(arr)` returns `NaN`. `Math.max()` expects comma-separated arguments, but not an array. The spread operator makes this syntax much better to read and maintain.

```js
const arr = [6, 89, 3, 45];
const maximus = Math.max(...arr);
```

`maximus` would have a value of `89`.

`...arr` returns an unpacked array. In other words, it _spreads_ the array. However, the spread operator only works in-place, like in an argument to a function or in an array literal. The following code will not work:

```js
const spreaded = ...arr;
```



### Destructuring

#### Use Destructuring Assignment to Extract Values from Objects

Destructuring is **a JavaScript expression that allows us to extract data from arrays, objects, and maps and set them into new, distinct variables**. Destructuring allows us to extract multiple properties, or items, from an array​ at a time.

Destructuring assignment is special syntax introduced in ES6, for neatly assigning values taken directly from an object.

Consider the following ES5 code:

```js
const user = { name: 'John Doe', age: 34 };

const name = user.name;
const age = user.age;
```

`name` would have a value of the string `John Doe`, and `age` would have the number `34`.

Here's an equivalent assignment statement using the ES6 destructuring syntax:

```js
const { name, age } = user;
```

Again, `name` would have a value of the string `John Doe`, and `age` would have the number `34`.

Here, the `name` and `age` variables will be created and assigned the values of their respective values from the `user` object. You can see how much cleaner this is.

You can extract as many or few values from the object as you want.


```js
const HIGH_TEMPERATURES = {
yesterday: 75,
today: 77,
tomorrow: 80

};

const { today, tomorrow} = HIGH_TEMPERATURES;

  

// const today = HIGH_TEMPERATURES.today;

// const tomorrow = HIGH_TEMPERATURES.tomorrow;
```

#### Use Destructuring Assignment to Assign Variables from Objects

Destructuring allows you to assign a new variable name when extracting values. You can do this by putting the new name after a colon when assigning the value.

Using the same object from the last example:

```js
const user = { name: 'John Doe', age: 34 };
```

Here's how you can give new variable names in the assignment:

```js
const { name: userName, age: userAge } = user;
```

You may read it as "get the value of `user.name` and assign it to a new variable named `userName`" and so on. The value of `userName` would be the string `John Doe`, and the value of `userAge` would be the number `34`.

```js
const HIGH_TEMPERATURES = {
yesterday: 75,
today: 77,
tomorrow: 80

};

//const highToday = HIGH_TEMPERATURES.today;
//const highTomorrow = HIGH_TEMPERATURES.tomorrow;

const {today:highToday, tomorrow:highTomorrow} = HIGH_TEMPERATURES;
```

#### Use Destructuring Assignment to Assign Variables from Nested Objects

You can use the same principles from the previous two lessons to destructure values from nested objects.

Using an object similar to previous examples:

```js
const user = {
  johnDoe: { 
    age: 34,
    email: 'johnDoe@freeCodeCamp.com'
  }
};
```

Here's how to extract the values of object properties and assign them to variables with the same name:

```js
const { johnDoe: { age, email }} = user;
```

And here's how you can assign an object properties' values to variables with different names:

```js
const { johnDoe: { age: userAge, email: userEmail }} = user;
```


#### Use Destructuring Assignment to Assign Variables from Nested Objects

You can use the same principles from the previous two lessons to destructure values from nested objects.

Using an object similar to previous examples:

```js
const user = {
  johnDoe: { 
    age: 34,
    email: 'johnDoe@freeCodeCamp.com'
  }
};
```

Here's how to extract the values of object properties and assign them to variables with the same name:

```js
const { johnDoe: { age, email }} = user;
```

And here's how you can assign an object properties' values to variables with different names:

```js
const { johnDoe: { age: userAge, email: userEmail }} = user;
```

```js
const LOCAL_FORECAST = {
yesterday: { low: 61, high: 75 },
today: { low: 64, high: 77 },
tomorrow: { low: 68, high: 80 }
};

//const lowToday = LOCAL_FORECAST.today.low;
//const highToday = LOCAL_FORECAST.today.high;

const {today: {low:lowToday, high:highToday}} = LOCAL_FORECAST;
```

#### Use Destructuring Assignment to Assign Variables from Arrays

ES6 makes destructuring arrays as easy as destructuring objects.

One key difference between the spread operator and array destructuring is that the spread operator unpacks all contents of an array into a comma-separated list. Consequently, you cannot pick or choose which elements you want to assign to variables.

Destructuring an array lets us do exactly that:

```js
const [a, b] = [1, 2, 3, 4, 5, 6];
console.log(a, b);
```

The console will display the values of `a` and `b` as `1, 2`.

The variable `a` is assigned the first value of the array, and `b` is assigned the second value of the array. We can also access the value at any index in an array with destructuring by using commas to reach the desired index:

```js
const [a, b,,, c] = [1, 2, 3, 4, 5, 6];
console.log(a, b, c);
```

The console will display the values of `a`, `b`, and `c` as `1, 2, 5`.



#### Use Destructuring Assignment with the Rest Parameter to Reassign Array Elements

In some situations involving array destructuring, we might want to collect the rest of the elements into a separate array.

The result is similar to `Array.prototype.slice()`, as shown below:

```js
const [a, b, ...arr] = [1, 2, 3, 4, 5, 7];
console.log(a, b);
console.log(arr);
```

The console would display the values `1, 2` and `[3, 4, 5, 7]`.

Variables `a` and `b` take the first and second values from the array. After that, because of the rest parameter's presence, `arr` gets the rest of the values in the form of an array. The rest element only works correctly as the last variable in the list. As in, you cannot use the rest parameter to catch a subarray that leaves out the last element of the original array.

```js
const source = [1,2,3,4,5,6,7,8,9,10];
function removeFirstTwo(list) {
// Only change code below this line

const [a,b,...arr] = list; // Change this line

// Only change code above this line

return arr;

}

const arr = removeFirstTwo(source);
```


#### Use Destructuring Assignment to Pass an Object as a Function's Parameters

In some cases, you can destructure the object in a function argument itself.

Consider the code below:

```js
const profileUpdate = (profileData) => {
  const { name, age, nationality, location } = profileData;

}
```

This effectively destructures the object sent into the function. This can also be done in-place:

```js
const profileUpdate = ({ name, age, nationality, location }) => {

}
```

When `profileData` is passed to the above function, the values are destructured from the function parameter for use within the function.


```js
const stats = {
max: 56.78,
standard_deviation: 4.34,
median: 34.54,
mode: 23.87,
min: -0.75,
average: 35.85
};

//const half = (stats) => (stats.max + stats.min) / 2.0;
const half = ({max, min}) => (max+min) / 2.0;
```





Imagine you'd like to extract some properties of an object. In a pre-ES2015 environment, you would need to write the following code:


```js
var hero = {
name: 'Batman',
realName: 'Bruce Wayne'
};

var name = hero.name;
var realName = hero.realName;

name; // => 'Batman',
realName; // => 'Bruce Wayne'
```

That's where the object destructuring syntax is useful: you can read a property and assign its value to a variable without duplicating the property name. More than that, you can read multiple properties from the same object in just one statement!

destructure

```js
const hero = {
name: 'Batman',
realName: 'Bruce Wayne'
};

const { name, realName } = hero;

name; // => 'Batman',
realName; // => 'Bruce Wayne'
```


```js

const name     = hero.name;  
const realName = hero.realName;  
// is equivalent to:  

const { name, realName } = hero;   `

```


The basic syntax of object destructuring is pretty simple:

```js
const { identifier } = expression;
```

Where `identifier` is the name of the property to access and `expression` should evaluate to an object. After the destructuring, the variable `identifier` contains the property value.

Here's the equivalent code using a property accessor

`   const identifier = expression.identifier;   `

Let's try the object destructuring in practice:

```js
const hero = {    name: 'Batman',    realName: 'Bruce Wayne'  };  
const { name } = hero;  
name; // => 'Batman'   
```
The statement `const { name } = hero` defines the variable `name` and initializes it with the value of `hero.name` property.



## Extracting multiple properties

To destructure the object into multiple properties, enumerate as many properties as you like adding commas `,` in-between:

```js
const { identifier1, identifier2, ..., identifierN } = expression;
```

Where `identifier1`, ..., `identifierN` are names of properties to access, and `expression` should evaluate to an object. After the destructuring, the variables `identifier1`, ..., `identifierN` contain corresponding properties values.

Here's the equivalent code:

```js
const identifier1 = expression.identifier1;  
const identifier2 = expression.identifier2;  

// ...  const identifierN = expression.identifierN;   
```

Let's take a look again at the example from the first section, where 2 properties are extracted:

```js
const hero = {    name: 'Batman',    realName: 'Bruce Wayne'  }; 
const { name, realName } = hero;  name;     

// => 'Batman',  realName; 
// => 'Bruce Wayne' 
```  

`const { name, realName } = hero` creates 2 variables `name` and `realName` assigned with values of corresponding properties `hero.name` and `hero.realName`.


## Aliases

If you'd like to create variables of different names than the properties, then you can use the aliasing feature of object destructuring.

```js
const { identifier: aliasIdentifier } = expression;   `
```

`identifier` is the name of the property to access, `aliasIdentifier` is the variable name, and `expression` should evaluate to an object. After the destructuring, the variable `aliasIdentifier` contains the property value.

The equivalent code:

```js
const aliasIdentifier = expression.identifier; 
```

Here's an example of object destructuring alias feature:

```js
const hero = { name: 'Batman',    
			  realName: 'Bruce Wayne'  
			  };  
			  
const { realName: secretName } = hero;  

secretName; // => 'Bruce Wayne
```  

Looking at `const { realName: secretName } = hero`, the destucturing defines a new variable `secretName` (alias variable), and assigns to it the value `hero.realName`.


## Extracting properties from nested objects


Here's the basic syntax:

```js

const { nestedObjectProp: { identifier } } = expression;

```   

`nestedObjectProp` is the name of the property that holds a nested object. `identifier` is the property name to access from the nested object. `expression` should evaluate to the destructured object.

After the destructuring, the variable `identifier` contains the property value of the nested object.

The above syntax is equivalent to:

```js
const identifier = expression.nestedObjectProp.identifier; 

```

