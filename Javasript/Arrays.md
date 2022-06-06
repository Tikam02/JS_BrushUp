


### Accessing Arrays examples:


```js
let todoList = [
{item_name:"Apple", price:"$5", quantity:1, brand_details: {name:"Golden Delicious", location:"San Francisco"}, isChecked:true},

{item_name:"Bannana", price:"$3", quantity:2, brand_details: {name:"Fuji", location:"San Diego"}, isChecked:false},

{item_name:"Pears", price:"$7", quantity:4, brand_details: {name:"Golden Delicious", location:"San Francisco"}, isChecked:true},

{item_name:"Milk", price:"$4", quantity:3, brand_details: {name:"Mother Dairy", location:"California"}, isChecked:false},

];
```

```js
todoList.map( ({item_name,price, quantity}) => {
	console.log(`${item_name} with quantity ${quantity} with price ${price}`)
});


todoList.map( ({item_name,isChecked,brand_details:{name}}) => {
	if(isChecked){
console.log(`${item_name} from ${name} is selected`)
	}
})
```


**Transforming Array of Objects using map()**


The main function of Array.map() is to **transform an array into a new array with different values**. The entries for the transformed array are returned from the callback function of Array.map().

```js
// Transform into nested array of item_name with isChecked value 
todoList.map(({item_name, isChecked})=>{ 
  return [item_name, isChecked];
});

// [["Apple", true]
//  ["Bannana", false]
//  ["Pears", true]
//  ["Milk", false]]

// Transform into array of objects with item_name and price 

todoList.map(({item_name, price})=>{ 
  return {item_name, price};

});

// [{item_name: "Apple", price: "$5"}
//  {item_name: "Bannana", price: "$3"}
//  {item_name: "Pears", price: "$7"}
//  {item_name: "Milk", price: "$4"}]
```


 **Creating List from Array of Objects**

A **list of all property values** from the array of objects can be retrieved using Array.map() by returning the property value in the callback function. In the below example we create an **array of all item_name values** using Array.map() on todoList declaration. The second example demonstrates creating an **array of brand location values** which is very similar to the first with another level of de-structuring for accessing brand location value.



```js
// Print all item_name values from array of objects

const itemList = todoList.map(({item_name})=> item_name);
	console.log(itemList)

// ["Apple", "Bannana", "Pears", "Milk"]

// Print unique brand location values from array of objects
let productLocations = todoList.map(({brand_details: {location}}) => location);

productLocations = new Set(productLocations)

console.log(productLocations)

// {"San Francisco", "San Diego", "California"}
```







 **Add Property to Array of Object**

In order to add a new property to every object from the array of objects, the **transformed object with a new property value has to be returned** in the Array.map() callback function. We use the JavaScript **spread operator to include all existing object** property values along with the new properties that need to be added to object entries.

```js
// Adding "total" property to todoList objects

todoList = todoList.map(

(item)=> { 

  // Parsing price string to number value

  const price = Number(item.price.replace("$", ""))

  return {...item, total: `\$${price*item.quantity}`}

});

console.log(todoList)
```



**Delete Property from Array of Object**

There are **two approaches to delete a property** from an array of objects using Array.map(), they are as follows:

1.  Update array with new transformed array by **returing an object without the property** in the callaback function inside Array.map().
2.  Iterate over every object and perform “**delete object.property_name**” to permanently delete the property from the reference object.


```js
// Transform array to exclude brand_details property from todoList

todoList = todoList.map(

 ({item_name, price, quantity, isChecked})=> { 

   return { item_name, price, quantity, isChecked }

});

console.log(todoList)

//[{item_name: "Apple", price: "$5", quantity: 1}
// {item_name: "Bannana", price: "$3", quantity: 2}
// {item_name: "Pears", price: "$7", quantity: 4}
// {item_name: "Milk", price: "$4", quantity: 3}]

// Delete price property for every object entry in todoList

todoList = todoList.map(

(item)=> {  

  delete item.price 

  return item;

});

console.log(todoList)

// [{item_name: "Apple", quantity: 1}
// {item_name: "Bannana", quantity: 2}
// {item_name: "Pears", quantity: 4}
// {item_name: "Milk", quantity: 3}]"
```


 **Accessing each Key/Value Pair in Array of Objects**

The key/value pairs of object entries can be accessed using **Object.entries()** method alternatively, the list of keys/values can be accessed individually using **Object.keys()** and **Object.values()**.



### Array Push()

The **`push()`** method adds one or more elements to the end of an array and returns the new length of the array.

```
const animals = ['pigs', 'goats', 'sheep'];

const count = animals.push('cows');
console.log(count);
// expected output: 4
console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows"]

animals.push('chickens', 'cats', 'dogs');
console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows", "chickens", "cats", "dogs"]

```



### How to merge Arrays in Javascript 


#### Immutable merge of arrays

##### 1.1 Merge using the spread operator

```js
const heroes = ['Batman', 'Superman'];

const villains = ['Joker', 'Bane'];

const all = [...heroes, ...villains];

all; // ['Batman', 'Superman', 'Joker', 'Bane']
```


`const all = [...heros, ...villains]` creates a new array having `heroes` and `villains` arrays merged.



The spread operator approach lets you merge 2 and even more arrays at once:

```const mergeResult = [...array1, ...array2, ...array3, ...arrayN];   ```


#### 1.2 Merge using _array.concat()_ method

If you prefer a functional way to merge arrays, then you can use the `array1.concat(array2)` method:

`array.concat()` method doesn't mutate the array upon which it is called but returns a new array having the merge result.


```js
const heroes = ['Batman', 'Superman'];

const villains = ['Joker', 'Bane'];

const all1 = heroes.concat(villains);

const all2 = [].concat(heroes, villains);

all1; // ['Batman', 'Superman', 'Joker', 'Bane']

all2; // ['Batman', 'Superman', 'Joker', 'Bane']
```

The concat method accepts multiple arrays as arguments, thus you can merge 2 or more arrays at once:

`   const mergeResult = [].concat(array1, array2, array3, arrayN);   `


### Mutable merge of arrays


#### Merge using _array.push()_ method

`array.push(item)` method pushes an item at the end of the array, mutating the array upon which the method is called:

```js
const heroes = ['Batman'];  

heroes.push('Superman');  

heroes; // ['Batman', 'Superman']  
``` 


```js
const heroes = ['Batman', 'Superman'];

const villains = ['Joker', 'Bane'];

heroes.push(...villains);

heroes; // ['Batman', 'Superman', 'Joker', 'Bane']
```