title: object to array
---

[transform object to array with lodash](https://stackoverflow.com/questions/24674630/transform-object-to-array-with-lodash)

A modern native solution if anyone is interested:  
```js
const arr = Object.keys(obj).map(key => ({ key, value: obj[key] }));
```