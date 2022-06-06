

## Basic Hooks

1.  **useState()**
2.  **useEffect()**
3.  **useContext()**

## Aditional Hooks

1.  **useReducer()**
2.  **useRef()**
3.  **useCallback()**
4.  **useMemo()**



**Plain Javascript State


State describes the status of the entire program or an individual object. It could be text, a number, a boolean, or another data type.
It’s a common tool for coordinating code. For example, once you update state, a bunch of different functions can instantly react to that change.




### UseContext()


####  Context


Context APIs enable us to **define the context Object which stores some data and will make it available throughout the hierarchy without passing the data as props**. To Simplify, context provides a container containing some data and making it available to the entire hierarchy of components below.

First, you have to create the React Context itself which gives you access to a Provider and Consumer component. When you create the context with React by using `createContext`, you can pass it an initial value. The initial value can be null too.

```js
// src/ThemeContext.js

import React from 'react';
const ThemeContext = React.createContext(null);
export default ThemeContext;
```

```js

          +----------------+
          |                |
          |       A        |
          |                |
          |     Provide    |
          |       Theme    |
          +--------+-------+
                   |
         +---------+-----------+
         |                     |
         |                     |
+--------+-------+    +--------+-------+
|                |    |                |
|                |    |                |
|       B        |    |        D       |
|                |    |                |
|                |    |                |
+----------------+    +--------+-------+
                               |
                      +--------+-------+
                      |                |
                      |                |
                      |        E       |
                      |                |
                      |                |
                      +--------+-------+
                               |
                      +--------+-------+
                      |                |
                      |        C       |
                      |                |
                      |     Consume    |
                      |       Theme    |
                      +----------------+
```

Second, component A would have to provide the context with the given Provider component. In this case, its `value` is given to it right away, but it can be anything from component state (e.g. [fetched data](https://www.robinwieruch.de/react-fetching-data/)) to props. If the value comes from a modifiable [React State](https://www.robinwieruch.de/react-state/), the value passed to the Provider component can be changed too.

```js

// src/ComponentA.js
import React from 'react';
import ThemeContext from './ThemeContext';

const A = () => (
  <ThemeContext.Provider value="green">
    <D />
  </ThemeContext.Provider>

);
```



Component A displays only component D, doesn't pass any props to it though, but rather makes the value `green` available to all the React components below. One of the child components will be component C that consumes the context eventually.

Third, in your component C, below component D, you could consume the context object. Notice that component A doesn’t need to pass down anything via component D in the props so that it reaches component C.

```js
// src/ComponentC.js
import React from 'react';
import ThemeContext from './ThemeContext';

const C = () => (
  <ThemeContext.Consumer>
    {value => (
      <p style={{ color: value }}>
        Hello World
      </p>
    )}
  </ThemeContext.Consumer>

);
```


Example:


```js
import React, { useState } from "react";


function UserDetailsComponent() {
var [userDetails, setUserDetails] = useState({
	name: "Mayank",
	age: 30
});
	return(
		<div>
			<h1>This is the Parent Component</h1><hr/>
			<ChildComponent userDetails={userDetails}></ChildComponent>
		</div>
	)

}

function ChildComponent(props) {
	return (

	<div>
		<h2>This is Child Component</h2><hr/>
		<SubChildComponent userDetails={props.userDetails}></SubChildComponent>
	</div>
	)
}

function SubChildComponent(props) {
	return (
	<div>
		<h3>This is Sub Child Component</h3>
		<h4>User Name: {props.userDetails.name}</h4>
		<h4>User Age: {props.userDetails.age}</h4>
	</div>
	)
}
```

Problem With Props:


1.  The state data is defined at the top level, the defined data is passed to the child component, where the data is not getting used again. The data from the parent is passed as “props” data. This “props” data has no impact on the child component, but still, the child component needs to maintain the props data.
2.  “ChildComponent” further passes this “props” data to the “SubChildComponent”. “ChildComponent” here maintains an overhead to manage the props from the parent component, just to make it available to the further child components
3.  We need to explicitly keep passing the “props” to even those components which do not even use it only to make the data available to the hierarchy below. We are maintaining the overhead of constantly passing the “props” data throughout the entire Hierarchy.


**useContext Provider


```js
  
import React, { useState } from "react";

var userDetailContext = React.createContext(null);
export default function UserDetailsComponent() {
var [userDetails] = useState({
	name: "Mayank",
	age: 30
});

return (
	<userDetailContext.Provider value={userDetails}>
		<h1>This is the Parent Component</h1>
		<hr />
		<ChildComponent userDetails={userDetails} />
	</userDetailContext.Provider>
	);
}
```


**useContext Consumer


```js

import React, { useState } from "react";
var userDetailContext = React.createContext(null);
export default function UserDetailsComponent() {

var [userDetails] = useState({
	name: "Mayank",
	age: 30
});

return (
	<userDetailContext.Provider value={userDetails}>
		<h1>This is the Parent Component</h1>
		<hr />
		<ChildComponent userDetails={userDetails} />
	</userDetailContext.Provider>
	);
}

function ChildComponent(props) {
	return (

		<div>
			<h2>This is Child Component</h2>
			<hr />
			<SubChildComponent />
		</div>
	);
}

function SubChildComponent(props) {

var contextData = React.useContext(userDetailContext);

	return (
	<div>
		<h3>This is Sub Child Component</h3>
		<h4>User Name: {contextData.name}</h4>
		<h4>User Age: {contextData.age}</h4>
	</div>
	);
}
```


### UseState


-   In useState, we set the **initial state** of the state variable and use **useState defined function** to change that state of that state variable from the **initial state** to the **current state**.
-   We can only use **useState** in **functional components,** not in **class-based components**
- the useState hooks lets us store “state” as data, which our functional components can use

Plain Function of UseState()

```javascript
const useState = (defaultValue) => {
  // 👆 We create a function useState with a default value
  let value = defaultValue;
  // 👆 We create a local variable value = defaultValue
  const getValue = () => value
  // 👇 We create a function to set the value with parameter newValue
  const setValue = newValue => value = newValue // 👈 We change the value for newValue
  return [getValue, setValue]; // 👈 We return an array with the value and the function
}

const [counter, setCounter] = useState(0);
// 👆 We destructure the array as a return of the useState function into two value

console.log(counter()); // 👈 returns 0 which it's the value of counter()
```

```javascript
function useState(defaultValue) {
  let value = defaultValue

  function getValue() {
    return value
  }

  function setValue(newValue) {
    value = newValue
  }

  return [getValue, setValue];
}

const [counter, setCounter] = useState(0);
```


Syntax:

```jsx
const [number, setNumber] = useState(5);
```


Example:


```js
import {useState} from 'react'

function App() {
// Defining state-variable(count) and state-function(setCount) that will change the state of state variable
const [count,setCount] = useState(0)

// Will decreament the count variable by one
const decreament = () => {
	setCount(count-1)
}

// Will increament the count variable by one
const increament = () => {
	setCount(count+1)
}

return (

<div className="App" style={{fontFamily:'sans-serif',textAlign:'center'}}>
	<h1>Counter using useState Hook</h1>
	<h3>Counter Value is {count}</h3>
	<button onClick = {increament} >Increament +</button>
	<button onClick = {decreament} >Decreament -</button>
</div>

);

}

export default App;
```



Adding state to a functional component requires 4 steps: _enabling_ the state, _initializing_, _reading_ and _updating_.


#### 1. Showing/hiding things

```jsx
import React, { useState } from 'react';

export default function App() {
	const [showText, setShowText] = useState(false);

	return (
		<div className='App'>
			<button onClick={() => setShowText(!showText)}>Toggle Text</button>

			{showText && <div>This text will show!</div>}
		</div>
	);
}
```

#### 2. Conditional Rendering

```jsx
import React, { useState } from 'react';

function SignInScreen() {
	return <div>Please login!</div>;
}

function DashboardScreen() {
	return <div>Hello! Welcome to your dashboard</div>;
}

export default function App() {
	const [isLoggedIn, setIsLoggedIn] = useState(false);

	return <div className='App'>{isLoggedIn ? <DashboardScreen /> : <SignInScreen />}</div>;
}
```


#### 3. Holding a list of data


```jsx
import React, { useState } from 'react';

export default function App() {
	const [todos, setTodos] = useState([
		{ description: 'First thing on the list', isComplete: false },
		{ description: 'Second thing on the list', isComplete: false },
		{ description: 'Last thing todo', isComplete: false },
	]);

	return (
		<>
			{todos.map((todo) => (
				<div>
					Description:
					{todo.description} - Completed:
					{todo.isComplete.toString()}
				</div>
			))}
		</>
	);
}
```


#### 4. Holding form values

```jsx
import React, { useState } from 'react';

export default function App() {
	const [username, setUsername] = useState("");
	const [password, setPassword] = useState("");

	const handleFormSubmit = () => {
		alert(`username is ${username}, password is ${password}`);
	};

	return (
		<>
			<form onSubmit={handleFormSubmit}>
				Username:
				<input value={username} onChange={(e) => setUsername(e.target.value)} />
				Password:
				<input value={password} onChange={(e) => setPassword(e.target.value)} />
				<button type='submit'>Submit</button>
			</form>
		</>
	);
}
```






-----------------------------------------------------------------------

refs:

- https://btholt.github.io/complete-intro-to-react-v5/hooks-in-depth
- https://jschris.com/what-is-the-usestate-hook-with-examples
- https://medium.com/edonec/state-in-react-an-overview-a182675cee2c


### UseRef()

useRef is a hook which returns an object with a current property set to the value passed to the hook.

There are two main uses of the useRef hook.

The first being for **interacting with the browser DOM** directly to make changes, rather than letting React manage things through the virtual DOM.

The second use you might see is for creating an object with values which persist between renders.

useRef creates an object that will hold on to values even when state changes and the component re-renders. This makes it very useful for doing things like tracking the previous state or counting how many times a state changes.

It is a function which takes a maximum of one argument and returns an `Object`. The returned object has a property called `current` whose value is the argument passed to `useRef`. If you invoke it without an argument, the returned object's `current` property is set to `undefined`.

Some of the use cases of `useRef` hook are:

1.  To access DOM elements
2.  To persist values in successive renders


### UseEffect()

`useEffect()` hook accepts 2 arguments:

`   useEffect(callback[, dependencies]);   `

-   `callback` is the function containing the side-effect logic. `callback` is executed right after changes were being pushed to DOM.
-   `dependencies` is an optional array of dependencies. `useEffect()` executes `callback` only if the dependencies have changed between renderings.

Put your side-effect logic into the `callback` function, then use the `dependencies` argument to control when you want the side-effect to run. That's the sole purpose of `useEffect()`._

Syntax:

```js
useEffect(
    () => {
        // execute side effect
    },
    // optional dependency array
    [
        // 0 or more entries
    ] 
)
```






```jsx
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {    document.title = `You clicked ${count} times`;  });
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```


**how does the effect read the latest `count` state?**


**It’s not the `count` variable that somehow changes inside an “unchanging” effect. It’s the _effect function itself_ that’s different on every render**


```jsx
// During first render
function Counter() {
  // ...
  useEffect(
    // Effect function from first render    
    () => {      
    document.title = `You clicked ${0} times`;    }  );
  // ...
}

// After a click, our function is called again
function Counter() {
  // ...
  useEffect(
    // Effect function from second render    
    () => {      
    document.title = `You clicked ${1} times`;    }  );
  // ...
}

// After another click, our function is called again
function Counter() {
  // ...
  useEffect(
    // Effect function from third render    
    () => {      
    document.title = `You clicked ${2} times`;    }  );
  // ..
}
```

**Conceptually, you can imagine effects are a _part of the render result_.**

 what happens after we click:

-   **Your component:** Hey React, set my state to `1`.
-   **React:** Give me the UI for when the state is `1`.
-   **Your component:**
    
    -   Here’s the render result: `<p>You clicked 1 times</p>`.
    -   Also remember to run this effect after you’re done: `() => { document.title = 'You clicked 1 times' }`.
-   **React:** Sure. Updating the UI. Hey browser, I’ve changed the DOM.
-   **Browser:** Cool, I painted your changes to the screen.
-   **React:** OK, now I’ll run the effect that belongs to the render I just did.
    
    -   Running `() => { document.title = 'You clicked 1 times' }`.




There are two strategies to be honest about dependencies. You should generally start with the first one, and then apply the second one if needed.

- **The first strategy is to fix the dependency array to include _all_ the values inside the component that are used inside the effect.**
- **The second strategy is to change our effect code so that it wouldn’t _need_ a value that changes more often than we want.** We don’t want to lie about the dependencies — we just want to change our effect to have _fewer_ of them.


```jsx
useEffect(() => {
  const id = setInterval(() => {
    setCount(count + 1);  }, 1000);
  return () => clearInterval(id);
}, [count]);
```

This makes the dependency array correct. It may not be _ideal_ but that’s the first issue we needed to fix. Now a change to `count` will re-run the effect, with each next interval referencing `count` from its render in `setCount(count + 1)`:


```jsx
// First render, state is 0
function Counter() {
  // ...
  useEffect(
    // Effect from first render
    () => {
      const id = setInterval(() => {
        setCount(0 + 1); // setCount(count + 1)      }, 1000);
      return () => clearInterval(id);
    },
    [0] // [count]  );
  // ...
}

// Second render, state is 1
function Counter() {
  // ...
  useEffect(
    // Effect from second render
    () => {
      const id = setInterval(() => {
        setCount(1 + 1); // setCount(count + 1)      }, 1000);
      return () => clearInterval(id);
    },
    [1] // [count]  );
  // ...
}
```



##### `dependencies` argument of `useEffect(callback, dependencies)` lets you control when the side-effect runs. When dependencies are:


A) Not provided: the side-effect runs after _every_ rendering.

```js
import { useEffect } from 'react';
function MyComponent() {
	useEffect(() => {
// Runs after EVERY rendering
	});
}
```

B) An empty array `[]`: the side-effect runs _once_ after the initial rendering.

```js
import { useEffect } from 'react';
function MyComponent() {

useEffect(() => {
// Runs ONCE after initial rendering
	}, []);
}
```


C) Has props or state values `[prop1, prop2, ..., state1, state2]`: the side-effect runs _only when any depenendecy value changes_.

   
```js
import { useEffect, useState } from 'react';  

function MyComponent({ prop }) {    

const [state, setState] = useState('');    

useEffect(() => {      
	// Runs ONCE after initial rendering      
	// and after every rendering ONLY IF `prop` or `state` changes    
	}, [prop, state]);  
}

```







### UseReducer()


Why use useReducer() over useState()

>`useReducer` is usually preferable to `useState` when you have complex state logic that involves multiple sub-values or when the next state depends on the previous one. `useReducer` also lets you optimize performance for components that trigger deep updates because you can pass `dispatch` down instead of callbacks.
> - When the state consists of more than primitive values, like nested object or arrays.
> - Reducers are pure functions, and this means they have no side effects and must return the same outcome given the same arguments.






The `useReducer(reducer, initialState)` hook accept 2 arguments: the _reducer_ function and the _initial state_. The hook then returns an array of 2 items: the current state and the _dispatch_ function.

```js
import { useReducer } from 'react';

function MyComponent() {
	const [state, dispatch] = useReducer(reducer, initialState);
	
	const action = {
	type: 'ActionType'
	};

	return (
	<button onClick={() => dispatch(action)}>
		Click me
	</button>
	);
}
```


**InitialState
>The _initial state_ is the value the state is initialized with.

```js
// initial state
const initialState = {
counter: 0

};
```


**Action Object

> **An _action object_ is an object that describes how to update the state.

Typically, the action object would have a property `type` — a string describing what kind of state update the reducer must do.

`   const action = {    type: 'increase'  };   `


here's an action object to add a new user to an array of users state:
```js
const action = {
	type: 'add',
	user: {
		name: 'John Smith',
		email: 'jsmith@mail.com'
	}
};
```


**Dispatch Function

>**The _dispatch_ is a special function that dispatches an action object.

`   const [state, dispatch] = useReducer(reducer, initialState);   `

Whenever you want to update the state (usually from an event handler or after completing a fetch request), you simply call the dispatch function with the appropriate action object: `dispatch(actionObject)`. 


**Reducer Function

>**The _reducer_ is a pure function that accepts 2 parameters: the _current state_ and an _action object_. Depending on the action object, the reducer function must update the state in an immutable manner, and return the new state.

```js
function reducer(state, action) {
	let newState;
	switch (action.type) {
		case 'increase':
			newState = { counter: state.counter + 1 };
			break;
		case 'descrease':
			newState = { counter: state.counter - 1 };
			break;
		default:
			throw new Error();
		}
	return newState;
}
```


**useReducer()

![](https://dmitripavlutin.com/5c33affee33e7c40e73028fb48a8367b/diagram.svg)



As a result of an event handler or after completing a fetch request, you call the _dispatch_ function with the _action object_.

Then React redirects the action object and the current state value to the _reducer_ function.

The reducer function uses the action object and performs a state update, returning the new state.

React then checks whether the new state differs from the previous one. If the state has been updated, React re-renders the component and `useReducer()` returns the new state value: `[newState, ...] = useReducer(...)`.

Note that `useReducer()` design is based on the [Flux architecture](https://facebook.github.io/flux/docs/in-depth-overview).


Example code:


```js
import React from 'react'
import { useReducer } from 'react'

  

const reducer = (state, action) =>{
	switch(action.type){
		case "DEPOSIT":
			return state + action.payload;
		case "WITHDRAW":
			return state - action.payload;
		}
};

  

export default function ComponentWithUseReducer() {
	const deposit = (amount) => {
		dispatch({type: "DEPOSIT",payload: amount,})
}

  
const withdraw = (amount) => {
		dispatch({type: "WITHDRAW",payload: amount,})
}


const [amount, dispatch] = useReducer(reducer,500);
	return (
		<div>
			<h1>{amount}</h1>
			<button onClick={() => deposit(500)}>Deposit</button>
			<button onClick={() => withdraw(500)}>Withdraw</button>
		</div>
	)
}
```













Reduce in Javascript 

- array.reduce(reducer, intialValue)
- singleValue = reducer(accumulator, itemValue)
- reduce method returns a single value


useReducer() in Javascript

- useReducer(reducer, intialState)
- newState = reducer(currentstate, action)
- useReducer returns a pair of values [newState, dispatch]







Refs:

- https://dmitripavlutin.com/react-usereducer/
- https://dev.to/spukas/3-reasons-to-usereducer-over-usestate-43adhttps://reactjs.org/docs/hooks-reference.html#usereducer
- https://dmitripavlutin.com/react-useeffect-explanation/
- https://daveceddia.com/useeffect-hook-examples/