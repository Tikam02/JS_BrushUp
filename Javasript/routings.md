


https://developer.mozilla.org/en-US/docs/Web/API/History/pushState
https://developer.mozilla.org/en-US/docs/Web/API/Window/popstate_event#The_popstate_event


## Location DOM


https://v5.reactrouter.com/web/api/location
https://surajsharma.net/blog/current-url-in-react
https://www.freecodecamp.org/news/react-router-cheatsheet/



## 1. Using window.location object

  

The simplest way to get the current URL and pathname in React is using a browser's window object.

```javascript
const currentURL = window.location.href // returns the absolute URL of a page

const pathname = window.location.pathname //returns the current url minus the domain name
```


## 2. React Router DOM

  

If your React App uses `react-router-dom` library for routing your single page application then there are few ways to extract the current pathname from the URL.

### Using location props
When you write,
```jsx
<Route path=”/home” component={Home} />
```


Implicity, `location`, `match` and `history` props are passed into the `Home` component.
These props can be accessed inside the `Home` component like this

```jsx
import React from 'react';

const Home = (props) => {
  console.log(props.location);
  console.log(props.match);
  console.log(props.history);
  return <></>;
}

export default Home;
```