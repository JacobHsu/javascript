title: String 類別
---

[String​.prototype​.toLower​Case()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)  

```js
function lowercase(str) {
    return str.charAt(0).toLowerCase() + str.slice(1);
}

console.log( lowercase('Hello') ) // "hello"
```

[String​.prototype​.replace()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/String/replace)  

```js
var str = 'hello put world';
var replaceStr = str.replace(/get|post|put|delete/, "");

console.log(replaceStr) // "hello  world"
```


## url 

[Array.join()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/join)  
```js
var url = 'http://3000';
const link = ["'",url,"'"].join('')
console.log(link); // => "'http://3000'"
```