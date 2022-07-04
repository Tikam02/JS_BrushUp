
Asynchornicity

An _asynchronous_ model allows multiple things to happen at the same time. When you start an action, your program continues to run. When the action finishes, the program is informed and gets access to the result (for example, the data read from disk).

### Eevent Loop

Event loop in javascript is responsible to decide which thing should be executed next. Here it uses some data structure to store functions.

1. Call Stack (LIFO)
2. Message Queue (FIFO)
3. Job Queue (FIFO)


```js
function main(){
	console.log("I'll have my breakfast");
	setTimeout(() => {
		console.log("I'll have my lunch");
	}, 0);

console.log("I'll have my dinner");
}

main();

// Output
// I'll have my breakfast
// I'll have my dinner
// I'll have my lunch
```

Here Call stack is empty so event loop will decide to execute things from the Message queue in FIFO way. So here console.log(“I’ll have my lunch”) will be executed at last.

Job queue is introduced in ES6 because of Promises. So the callbacks for promises are added into Job queue and all other callbacks are added in Message/Event queue. The priority for Job queue is high as compared to Message/Event queue.


### Callbacks

One approach to asynchronous programming is to make functions that perform a slow action take an extra argument, a _callback function_. The action is started, and when it finishes, the callback function is called with the result.

In JavaScript, you can also pass a function as an argument to a function. This function that is passed as an argument inside of another function is called a callback function.

```js
// function
function greet(name, callback) {
    console.log('Hi' + ' ' + name);
    callback();
}

// callback function
function callMe() {
    console.log('I am callback function');
}

// passing function as an argument
greet('Peter', callMe);
```


The benefit of using a callback function is that you can wait for the result of a previous function call and then execute another function call.

```js
// Callback Function Example
function greet(name, myFunction) {
    console.log('Hello world');

    // callback function
    // executed only after the greet() is executed
    myFunction(name);
}

// callback function
function sayName(name) {
    console.log('Hello' + ' ' + name);
}

// calling the function after 2 seconds
setTimeout(greet, 2000, 'John', sayName);
```


-----------------------------------------------------------------------


### Promise

>Promises in javascript is a way of solving dependencies at the time of API calls

A _promise_ is an asynchronous action that may complete at some point and produce a value. It is able to notify anyone who is interested when its value is available.

The easiest way to create a promise is by calling `Promise.resolve`. This function ensures that the value you give it is wrapped in a promise. If it’s already a promise, it is simply returned—otherwise, you get a new promise that immediately finishes with your value as its result.


In JavaScript, a promise is a good way to handle **asynchronous** operations. It is used to find out if the asynchronous operation is successfully completed or not.

A promise may have one of three states.

-   Pending
-   Fulfilled
-   Rejected

A promise starts in a pending state. That means the process is not complete. If the operation is successful, the process ends in a fulfilled state. And, if an error occurs, the process ends in a rejected state.

- A promise is a placeholder for a value that can either resolve or request at some time in the future.
- We create a promise, using a Promise constructor that recieves a callback
- A promise is an object that containes a status  ( Promise Status) and a Value (PromiseValue)

.then() gets called after a Promise is resolved
.catch() gets called after a Promise is rejected
.finally() Always gets called whether the promise resolved or rejected.

**Create A Promise

To create a promise object, we use the `Promise()` constructor.

```js
let promise = new Promise(function(resolve, reject){
     //do something
});
```



Basic Promise:

```js
// Resolved promise
let promise1 = new Promise((resolve, reject) => {
	resolve("Resolved this promise")
});

// Rejected promise

let promise2 = new Promise((resolve, reject) => {
	reject("Rejected the promise");
});
```


```js
const count = true;

let countValue = new Promise(function (resolve, reject) {
    if (count) {
        resolve("There is a count value.");
    } else {
        reject("There is no count value");
    }
});

console.log(countValue);
```


You can perform an operation after a promise is resolved using methods `then()`, `catch()` and `finally()`.


The syntax of `then()` method is:

```js
promiseObject.then(onFulfilled, onRejected);
```



**Why we need promise


Imagine a function, `createAudioFileAsync()`, which asynchronously generates a sound file given a configuration record and two callback functions, one called if the audio file is successfully created, and the other called if an error occurs.

```js
function successCallback(result) {
  console.log("Audio file ready at URL: " + result);
}

function failureCallback(error) {
  console.error("Error generating audio file: " + error);
}

createAudioFileAsync(audioSettings, successCallback, failureCallback);

```
If `createAudioFileAsync()` were rewritten to return a promise, you would attach your callbacks to it instead:

```js
createAudioFileAsync(audioSettings).then(successCallback, failureCallback);

```



With modern functions, we attach our callbacks to the returned promises instead, forming a promise chain:

```js

doSomething()
.then(function(result) {
  return doSomethingElse(result);
})
.then(function(newResult) {
  return doThirdThing(newResult);
})
.then(function(finalResult) {
  console.log('Got the final result: ' + finalResult);
})
.catch(failureCallback);

```



**then()

The `then()` method is used with the callback when the promise is successfully fulfilled or resolved.

```js
promiseObject.then(onFulfilled, onRejected);
```



```js
const count = 10;
let countValue = new Promise(function(resolve, reject){
	resolve("Promise Resolved");
});

countValue
	.then(function successValue(result){
	console.log(result)
})
	.then(function successValue1() {
	console.log("You can call multiple functions this way.");
});
```



**Catch()

The `catch()` method is used with the callback when the promise is rejected or if an error occurs. For example,


```js
// returns a promise
let countValue = new Promise(function (resolve, reject) {
   reject('Promise rejected'); 
});

// executes when promise is resolved successfully
countValue.then(
    function successValue(result) {
        console.log(result);
    },
 )

// executes if there is an error
.catch(
    function errorValue(result) {
        console.log(result);
    }
);
```



**JavaScript finally() method

You can also use the `finally()` method with promises. The `finally()` method gets executed when the promise is either resolved successfully or rejected.


```js
// returns a promise
let countValue = new Promise(function (resolve, reject) {
    // could be resolved or rejected   
    resolve('Promise resolved'); 
});

// add other blocks of code
countValue.finally(
    function greet() {
        console.log('This code is executed.');
    }
);
```


-----------------------------------------------------------------------

##### JavaScript Promise

1.  The syntax is user-friendly and easy to read.
2.  Error handling is easier to manage.
 Example
```js
    api().then(function(result) {
        return api2() ;
    }).then(function(result2) {
        return api3();
    }).then(function(result3) {
        // do work
    }).catch(function(error) {
        //handle any error that may occur before this point 
    });
```

###### JavaScript Callback

1.  The syntax is difficult to understand.
2.  Error handling may be hard to manage.

```js
api(function(result){
    api2(function(result2){
        api3(function(result3){
             // do work
            if(error) {
                // do something
            }
            else {
                // do something
            }
        });
    });
});
```


-----------------------------------------------------------------------


**Chaining


```js
const promise = doSomething();
const promise2 = promise.then(successCallback, failureCallback);

```

OR

```js
const promise2 = doSomething().then(successCallback, failureCallback);
```


 Each promise represents the completion of another asynchronous step in the chain.

Doing several asynchronous operations in a row would lead to the classic callback pyramid of doom:

```js
doSomething(function(result){
	doSomething(result,function(newResult){
		doSomething(result,function(finalResult){
			console.log('Got the final result:' + finalResult);
			},failureCallback);
		},failureCallback);
},failureCallback);
```

With modern functions, we attach our callbacks to the returned promises instead, forming a promise chain:

```js

doSomething()
	.then(function(result){
		return doSomethingElse(result);
	})
	.then(function(newResult){
		return doThirdThing(newResult);
	})
	.then(function(finalResult){
		console.log('Got the final result:' + finalResult);
	})
	.catch(failureCallback);
```

with Arrow Functions:

```js
doSomething()
	.then(result => doSomethingElse(result))
	.then(newResult => doThirdThing(newResult))
	.then(finalResult => {console.log(`Got the final Result:${finalResult}`)
	})
	.catch(failureCallback);
```

**Important:** Always return results, otherwise callbacks won't catch the result of a previous promise (with arrow functions `() => x` is short for `() => { return x; }`).



-----------------------------------------------------------------------

### Async/Await


We use the `async` keyword with a function to represent that the function is an asynchronous function. The async function returns a promise.


The syntax of `async` function is:

```js
async function name(parameter1, parameter2, ...paramaterN) {
    // statements
}
```

The `await` keyword is used inside the `async` function to wait for the asynchronous operation.

The syntax to use await is:

```js
let result = await promise;
```

Async functions works like this:

```js
async function myFirstAsyncFunction() {  
	try {  
		const fulfilledValue = await promise;  
		} catch (rejectedValue) {  
// …  
	}  
}
```

If you use the `async` keyword before a function definition, you can then use `await` within the function. When you `await` a promise, the function is paused in a non-blocking way until the promise settles. If the promise fulfills, you get the value back. If the promise rejects, the rejected value is thrown.



Logging fetch function Using Promise:

```js
const logFetch = (url) => {
	return fetch(url)
	.then(response => response.txt())
	.then(text => {console.log(text);})
	.catch(err => {console.error('fetch failed',err);});
}
```

And here's the same thing using async functions:


```js

const async logfetch = (url) =>{
	try{
	const response = await fetch(url);
	console.log(await response.text());
	}catch(err){
	console.log('fetch failed',err);
	}
}
```



#### Arrow functions 

```js
// map some URLs to json-promises
const jsonPromises = urls.map(async url => {  
	const response = await fetch(url);  
	return response.json();
});
```


#### Object methods

```js
const storage = {  async getAvatar(name) {    
	const cache = await caches.open('avatars');    
	return cache.match(`/avatars/${name}.jpg`);  
	}
};
storage.getAvatar('jaffathecake').then(…);
```

#### Class methods 

```js
class Storage {  
	constructor() {    
	this.cachePromise = caches.open('avatars');  
	}  
	async getAvatar(name) {    
	const cache = await this.cachePromise;    
	return cache.match(`/avatars/${name}.jpg`);  
	}
}
const storage = new Storage();
storage.getAvatar('jaffathecake').then(…);
```



Using Promise and Async Functions

```js
function resolveAfter2Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 2000);
  });
}

const asyncCall= async() => {
  console.log('calling');
  const result = await resolveAfter2Seconds();
  console.log(result);
  // expected output: "resolved"
}

asyncCall();

```





-----------------------------------------------------------------------

Refs:

https://web.dev/javascript-async-functions/
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function
https://eloquentjavascript.net/11_async.html
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises
https://www.programiz.com/javascript/callback
https://dev.to/lydiahallie/javascript-visualized-promises-async-await-5gke


