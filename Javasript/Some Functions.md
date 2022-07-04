
**To convert seconds to minutes and seconds:**

1.  Get the number of full minutes by dividing the seconds by `60`.
2.  Get the remainder of the seconds.
3.  Optionally, format the minutes as seconds as `mm:ss`.

```
const totalSeconds = 565;

// 👇️ get number of full minutes
const minutes = Math.floor(totalSeconds / 60);

// 👇️ get remainder of seconds
const seconds = totalSeconds % 60;

function padTo2Digits(num) {
  return num.toString().padStart(2, '0');
}

// ✅ format as MM:SS
const result = `${padTo2Digits(minutes)}:${padTo2Digits(seconds)}`;
console.log(result); // 👉️ "09:25"

```


```javascript
const milliseconds = 76329456;

const seconds = Math.floor(milliseconds / 1000);

console.log(seconds); // 76329
```


```javascript
const milliseconds = 76329456;

const seconds = Math.floor((milliseconds / 1000) % 60);

console.log(seconds); // 9
```


## [Convert to Minutes](https://sabe.io/blog/javascript-convert-milliseconds-seconds-minutes-hours#convert-to-minutes)

Using the same process as we did for seconds, we can get the minutes. This time we have to divide the milliseconds by `1000`, then by `60`, then modulus it by `60`.

Again, we want to use `Math.floor` to round the minutes down to the nearest whole number.

```javascript
const milliseconds = 76329456;

const seconds = Math.floor((milliseconds / 1000) % 60);

const minutes = Math.floor((milliseconds / 1000 / 60) % 60);

console.log(minutes); // 12
```


## [Convert to Hours](https://sabe.io/blog/javascript-convert-milliseconds-seconds-minutes-hours#convert-to-hours)

Finally, we can convert the milliseconds to hours. This time we have to divide the milliseconds by `1000`, then by `60`, then by `60` again.

However, this time we need to use modulus `24` since there are `24` hours in a day.

```javascript
const milliseconds = 76329456;

const seconds = Math.floor((milliseconds / 1000) % 60);

const minutes = Math.floor((milliseconds / 1000 / 60) % 60);

const hours = Math.floor((milliseconds / 1000 / 60 / 60) % 24);

console.log(hours); // 21
```