








**Value

A string representing the serialized content of the list. Each item is separated by a space.

The **`value`** property of the [`DOMTokenList`](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList) interface is a [stringifier](https://developer.mozilla.org/en-US/docs/Glossary/Stringifier) that returns the value of the list serialized as a string, or clears and sets the list to the given value.


```html
<span class="a b c"></span>
```


<span class="a b c"></span>
```html
const span = document.querySelector("span");
const classes = span.classList;
span.textContent = classes.value;

```

output:

```
a b c
```


