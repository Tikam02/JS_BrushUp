#### Create Strings using Template Literals

A new feature of ES6 is the template literal. This is a special type of string that makes creating complex strings easier.

Template literals allow you to create multi-line strings and to use string interpolation features to create strings.

Consider the code below:

```js
const person = {
  name: "Zodiac Hasbro",
  age: 56
};

const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;

console.log(greeting);
```

The console will display the strings `Hello, my name is Zodiac Hasbro!` and `I am 56 years old.`.

A lot of things happened there. Firstly, the example uses backticks (`` ` ``), not quotes (`'` or `"`), to wrap the string. Secondly, notice that the string is multi-line, both in the code and the output. This saves inserting `\n` within strings. The `${variable}` syntax used above is a placeholder. Basically, you won't have to use concatenation with the `+` operator anymore. To add variables to strings, you just drop the variable in a template string and wrap it with `${` and `}`. Similarly, you can include other expressions in your string literal, for example `${a + b}`. This new way of creating strings gives you more flexibility to create robust strings.









#### Complete a Promise with resolve and reject

A promise has three states: `pending`, `fulfilled`, and `rejected`. The promise you created in the last challenge is forever stuck in the `pending` state because you did not add a way to complete the promise. The `resolve` and `reject` parameters given to the promise argument are used to do this. `resolve` is used when you want your promise to succeed, and `reject` is used when you want it to fail.


```js

const myPromise = new Promise((resolve, reject) => {
  if(condition here) {
    resolve("Promise was fulfilled");
  } else {
    reject("Promise was rejected");
  }
});

```

```js
const makeServerRequest = new Promise((resolve, reject) => {
// responseFromServer is set to true to represent a successful response from a server

let responseFromServer = true;

if(responseFromServer) {

resolve("We got the data");

} else {

reject("Data not received");

}

});
```


Promises are most useful when you have a process that takes an unknown amount of time in your code (i.e. something asynchronous), often a server request. When you make a server request it takes some amount of time, and after it completes you usually want to do something with the response from the server. This can be achieved by using the `then` method. The `then` method is executed immediately after your promise is fulfilled with `resolve`.


`catch` is the method used when your promise has been rejected. It is executed immediately after a promise's `reject` method is called. Here’s the syntax:

```js
myPromise.catch(error => {
  
});
```

`error` is the argument passed in to the `reject` method.