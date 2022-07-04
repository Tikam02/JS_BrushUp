

## Data Transformation


**Array.filter

If we wanted to create a function that creates a new array of the schools that begin
with the letter “W,” we could use the Array.filter method:
```js
const wSchools = schools.filter(school => school[0] === "W");
console.log(wSchools);
// ["Washington & Liberty", "Wakefield"]
```
Array.filter is a built-in JavaScript function that produces a new array from a
source array. This function takes a predicate as its only argument. A predicate is a
function that always returns a Boolean value: true or false . Array.filter invokes
this predicate once for every item in the array. That item is passed to the predicate as
an argument, and the return value is used to decide if that item will be added to the
new array. In this case, Array.filter is checking every school to see if its name
begins with a “W.”


When it’s time to remove an item from an array, we should use Array.filter over
Array.pop or Array.splice because Array.filter is immutable. In this next sample,
the cutSchool function returns new arrays that filter out specific school names:

```js
const cutSchool = (cut, list) => list.filter(school => school !== cut);
console.log(cutSchool("Washington & Liberty", schools).join(", "));
// "Yorktown, Wakefield"
console.log(schools.join("\n"));
// Yorktown
// Washington & Liberty
// Wakefield
```

**Array.map

Let’s say we needed to transform the schools object into an array of schools:

```js
const schools = {
	Yorktown: 10,
	"Washington & Liberty": 2,
	Wakefield: 5
};

const schoolArray = Object.keys(schools).map((key) => ({
	name: key,
	wins: schools[key]
}));

console.log(schoolArray);
```


In this example, Object.keys returns an array of school names, and we can use map
on that array to produce a new array of the same length. The name of the new object
will be set using the key, and wins is set equal to the value.


**Array.reduce

The reduce and reduceRight functions can be used to transform an array into any
value, including a number, string, boolean, object, or even a function.
Let’s say we need to find the maximum number in an array of numbers. We need to
transform an array into a number; therefore, we can use reduce