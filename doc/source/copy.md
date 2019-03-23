title: Copy
---

物件跟基本型別最大的不同就在於他們的傳值方式


# 淺拷貝(Shallow Copy)

基本型別是傳 value

https://jsbin.com/lokejiveha/edit?js,console  
```js
var a = 10;
var b = a;
b = 20;

console.log(a); // 10
console.log(b); // 20
```

但物件就不同，物件傳的是 reference

https://jsbin.com/keholuroba/edit?js,console
```js
var obj1 = { a: 10, b: 20, c: 30 };
var obj2 = obj1;
obj2.b = 100;

console.log(obj1); // { a: 10, b: 100, c: 30 } <-- b 被改到了
console.log(obj2); // { a: 10, b: 100, c: 30 }
```

複製一份obj1叫做obj2  
然後把obj2.b改成100  
但卻不小心改到obj1.b  
因為他們根本是同一個物件，這就是所謂的`淺拷貝` 

# 深拷貝(Deep Copy)

https://jsbin.com/xeqevarisa/1/edit?js,console  
```js
var obj1 = { a: 10, b: 20, c: 30 };
var obj2 = { a: obj1.a, b: obj1.b, c: obj1.c };
obj2.b = 100;

console.log(obj1); // { a: 10, b: 20, c: 30 } <-- b 沒被改到
console.log(obj2); // { a: 10, b: 100, c: 30 }
```

但深拷貝會另外創造一個一模一樣的物件
新物件跟原物件不共用記憶體
修改新物件不會改到原物件


https://jsbin.com/venezeyonu/edit?js,console
```js  
var obj1 = { body: { a: 10 } };
var obj2 = { body: obj1.body };
obj2.body.a = 100;

console.log(obj1); // { body: { a: 100 } } <-- 被改到了
console.log(obj2); // { body: { a: 100 } }
console.log(obj1 === obj2); // false
console.log(obj1.body === obj2.body); // true
```

雖然obj1跟obj2是不同物件
但他們會共用同一個`obj1.body`
所以修改obj2.body.a時也會修改到舊的

## [Object.assign](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

https://jsbin.com/cejijipevo/edit?js,console

```js
var obj1 = { a: 10, b: 20, c: 30 };
var obj2 = Object.assign({}, obj1);
obj2.b = 100;

console.log(obj1); // { a: 10, b: 20, c: 30 } <-- 沒被改到
console.log(obj2); // { a: 10, b: 100, c: 30 }
```

`Object.assign({}, obj1)`的意思是先建立一個空物件{}
接著把obj1中所有的屬性複製過去
所以obj2會長得跟obj1一樣
這時候再修改obj2.b也不會影響obj1

因為Object.assign跟我們手動複製的效果相同  

## 轉成 JSON 再轉回來  

https://jsbin.com/kofawafune/edit?js,console
```js
var obj1 = { body: { a: 10 } };
var obj2 = JSON.parse(JSON.stringify(obj1));
obj2.body.a = 20;

console.log(obj1); // { body: { a: 10 } } <-- 沒被改到
console.log(obj2); // { body: { a: 20 } }
console.log(obj1 === obj2); // false
console.log(obj1.body === obj2.body); // false
```

這樣做是真正的 Deep Copy
但只有可以轉成JSON格式的物件才可以這樣用  
像function沒辦法轉成JSON
```js
var obj1 = { fun: function(){ console.log(123) } };
var obj2 = JSON.parse(JSON.stringify(obj1));

console.log(typeof obj1.fun); // 'function'
console.log(typeof obj2.fun); // 'undefined' <-- 沒複製
```