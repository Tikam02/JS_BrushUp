

## Props

**How state is different from props**: While props are just a vehicle to pass information down the component tree, state can be changed over time to create interactive user interfaces

#### REACT PROPS ARE JUST THE COMMUNICATION CHANNEL

A component receiving props does not know where and how the information originates -- it just sees a JavaScript object called props in React.

-   Where: The props can originate in the parent component or somewhere above the component hierarchy.
-   How: The information can be stateful or something else.


how to pass props:

```js

import * as React from 'react';
const App = () => {
  return (
    <div>
      <Welcome text="Welcome to React" />
    </div>
  );
};

const Welcome = (props) => {
  const { text } = props;
  return <h1>{text}</h1>;
};
```



Because we can destructure a JavaScript object in a function signature too, we can leave out the intermediate variable assignment:

```js
import * as React from 'react';
const App = () => {
  return (
    <div>
      <Welcome text="Welcome to React" />
    </div>
  );
};

const Welcome = ({ text }) => {
  return <h1>{text}</h1>;
```


If multiple props are passed to a child component, we can destructure all of them:


```js
import * as React from 'react';
const App = () => {
  return (
    <div>
      <Welcome text="Welcome to React" myColor="red" />
    </div>
  );
};

const Welcome = ({ text, myColor }) => {
  return <h1 style={{ color: myColor }}>{text}</h1>;
};
```



- A strategy for passing all properties of an object to a child component is using the [JavaScript spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax).

```js
import * as React from 'react';
const App = () => {
  const greeting = {
    title: 'React',
    description: 'Your component library for ...',
  };

  return (
    <div>
      <Welcome {...greeting} />
    </div>
  );
};

const Welcome = ({ title, description }) => {
  return (
    <div>
      <Headline title={`Welcome to ${title}`} />
      <Description paragraph={description} />
    </div>
  );
};

const Headline = ({ title }) => <h1>{title}</h1>;
const Description = ({ paragraph }) => <p>{paragraph}</p>;

export default App;
```




#### REACT'S CHILDREN PROP


The children prop in React can be used for composing React components into each other. Because of this feature, you can put JavaScript primitives or JSX between the opening and closing element's tags:


```js
import * as React from 'react';
const App = () => {
  const [count, setCount] = React.useState(0);
  return (
    <div>
      <Button onClick={() => setCount(count + 1)}>
        {count}
      </Button>
    </div>

  );

};
const Button = ({ onClick, children }) => (
  <button onClick={onClick}>{children}</button>
);

export default App;
```

here {count} is passed as children
In this case, only a string is put in between of the element's tags. Then in the child component, you can make use of everything which is in between of the tags by using **React's children prop**.


#### HOW TO PASS COMPONENTS AS PROPS

Before you have learned about React's children prop which allows you also to pass HTML/React element(s) to components as props:










##  Context


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

