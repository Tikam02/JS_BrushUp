

## Using Refs

One of these patterns involves accessing the DOM node directly using a
React feature called refs. In React, a ref is an object that stores values for the lifetime
of a component. There are several use cases that involve using refs. In this section,
we’ll look at how we can access a DOM node directly with a ref.
React provides us with a useRef hook that we can use to create a ref. We’ll use this
hook when building the AddColorForm component:

```js
import React, { useRef } from "react";
export default function AddColorForm({ onNewColor = f => f }) {
const txtTitle = useRef();
const hexColor = useRef();
const submit = e => { ... }
return (...)
}
```

First, when creating this component, we’ll also create two refs using the useRef hook.
The txtTitle ref will be used to reference the text input we’ve added to the form to
collect the color title. The hexColor ref will be used to access hexadecimal color val‐
ues from the HTML color input. We can set the values for these refs directly in JSX
using the ref property:

```js
return (
<form onSubmit={submit}>
<input ref={txtTitle} type="text" placeholder="color title..." required />
<input ref={hexColor} type="color" required />
<button>ADD</button>
</form>
);
}
```

Here, we set the value for the txtTitle and hexColor refs by adding the ref attribute
to these input elements in JSX. This creates a current field on our ref object that ref‐
erences the DOM element directly. This provides us access to the DOM element,
which means we can capture its value. When the user submits this form by clicking
the ADD button, we’ll invoke the submit function:
```js
const submit = e => {
e.preventDefault();
const title = txtTitle.current.value;
const color = hexColor.current.value;
onNewColor(title, color);
txtTitle.current.value = "";
hexColor.current.value = "";
};
```



## Context

React comes with a function called
createContext that we can use to create a new context object. This object contains
two components: a context Provider and a Consumer .



## UseEffect


useEffect's clean-up function doesn't _just_ run on unmount (assuming your dependency array isn't empty).

> Additionally, if a component renders multiple times (as they typically do), the previous effect is cleaned up before executing the next effect



```js
import React, { useEffect, useState } from 'react';

export default function App() {

  const [state, setState] = useState(null);

  useEffect(() => {

    console.log('I am the effect');

    return () => {

      console.log('I run after re-render, but before the next useEffect');

    };

  });

  console.log('I am just part of render');

  return (

    <>

      <button

        onClick={() => {

          setState('Some v. important state.');

        }}

      >

        Click me

      </button>

      <p>state: {state}</p>

    </>

  );

}
```




```js
import React, { useEffect } from 'react';
const SomeComponent => () => {
     useEffect(() => {
        return () => {
             // This code runs when the component unmounts
         }
     }, [])
     // The rest of your component goes here.
 }
```

## Effects Without cleanup

Some of the most common examples of effects that do not require clean-up are:

-   Manual DOM mutations
-   network requests
-   logging

These operations do not prevent the screen from being changed by the browser. We say that as we can control them and forget about them immediately.

Unlike `ComponentDidMount` or `ComponentDidUpdate`, the `UseEffect` schedule effects do not block the screen from being updated by the browser. This makes the application more responsive.

Basically, You can tell React that your component needs to do something after rendering by using this hook.

After performing the DOM updates, React will remember the feature you passed and later call it. When our component is rendered, it will remember the effect we used previously and run our effect after updating the DOM.


```js
import React, { useState, useEffect } from 'react';function Sample() {  
  const [rate, setRate] = useState(0);  useEffect(() => {  
    document.title = `You clicked ${rate} times`;  
  });  return (  
    <div>  
      <p>Hey!! you  have clicked {rate} times</p>  
      <button onClick={() => setRate(rate + 1)}>  
        Click  
      </button>  
    </div>  
  );  
}
```

## Effects with Cleanup

Some effects need cleanup after a DOM update happens.

```
useEffect(() => {  
  const subscription = props.source.subscribe();  
  return () => {  
    // Cleaning up the subscription  
    subscription.unsubscribe();  
  };  
});
```

In our example, this means every update creates a new subscription. So it is necessary to clean up memory so that we do not add a memory leak if we want to set up a subscription to any external data source.

So, the clean-up function runs before the component is eliminated from the UI to prevent memory leaks.

`UseEffect` is not only called when the item is unmounted. To clean up from the last run, it will run each time, even before the effect runs.