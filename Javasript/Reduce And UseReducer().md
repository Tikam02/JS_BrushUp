


Reduce => [accumulator(state), accumulator(action)]

.reduce() functions takes in two arguments, the accumulator(state) and the second is what you want to add to the accumulator(action). Basically combining these two things will give you third thing.


```js

[0,1,2,3,4].reduce((accumulate,currentValue) => {
	return accumulator+currentValue;
});
// 10
```


The .reduce() method takes in an argument of a callback function. This callback function takes in two arguments. The accumulator(in this case the sum) and the currentValue (in this case the next number in the array).

1st Iteration => accumulator = 0, currentValue = 0
					    accumulator = 1,  currentValue = 1
						accumulator = 1,  currentValue = 2
						accumulator = 3,  currentValue = 3
						accumulator = 6, currentValue  = 4
// 10


The reduce() method is used to apply a function to each element in the array to reduce the array to a single value.

let result = arr.reduce(callback);

//optionally, you can add initial value

let result = arr.reduce(Callback,initialvalue)

-> callback : the function to execute on each element in the array
-> InitialValue : an optionally supplied initial value, If this value is not supplies the 0th element is used as initialvalue


The callback function can take four arguments, three of them are from map() and filter() methods. The new argument is accumulator.

- Accumulator -> the accumulator accumulates all of the callback returned, gathers all the callback returned
- val -> the current value being processes
- index -> the current index of the value being processed
- arr -> the original array

Reduce Vs for loop

```js
var arr = [1,2,3,4]
var sum = 0;
for(var i=0; i<arr.length; i++){
	sum = sum+ arr[i];
}

//sum = 10
```

reduce()

```js
let sum = arr.reduce((acc,val) => {
	return acc+val;
})

//sum = 10

## With Initial Value

let sum = arr.reduce((acc,val) => {
	return acc+val;
},100)

//sum = 110
```



reducer function

we have initial value that we are passing in to a function that is then being combined with some additional data and producing a new value.

```js
const nums = [2,4,6]
const initialState = 0;

function reducer(state,value){
	return state + value;
}

const total = nums.reduce(reducer,intialstate);

//12
```


useReducer is similar to reduce, however there is one big difference instead of just returning the state, useReducer needs a way to invoke reducer function.

-> useReducer returns an array with the first element being the state and the second elemnet being a dispatch functions which when called will invoke reduce.

-> dispatch when called ----> invokes reducer function

const [state, dispatch] = useReducer(reducer, initialState);


when invoked, whatever you pass to dispatch will be passed as the second argument to the reducer. (which we have been calling val or values)

the first argument (which we have been calling state) will be passed implicitly by react and will be whatever the previous state values was.