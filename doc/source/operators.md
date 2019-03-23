title: Operators
---

++	Increment

後置遞增 `i++` 和前置遞增 `++i` 操作有什麼區別？  

他們都會使變量增加 1，只是計算和賦值的順序不一樣。

後置遞增是先賦值後計算，如：
```js
let i = 1;
console.log(i); //  1
let a = i++;
console.log(i); //  2
console.log(a); //  1
```
前置遞增是先計算後賦值，如：
```js
let i = 1;
console.log(i); //  1
let a = ++i;
console.log(i); //  2
console.log(a); //  2
```


https://jsbin.com/samaxubazo/edit?js,console  
```js
function aFunc(x) {
  return () => console.log(x++);
}
function bFunc(x) {
  return x++;
}
function cFunc(x) {
  return ++x;
}
let newFunc = aFunc(1)
newFunc() //1
newFunc() //2
newFunc() //3

console.log(bFunc(1)) //1
console.log(cFunc(1)) //2
```

references
===
https://www.w3schools.com/js/js_operators.asp
https://hacpai.com/article/1546665384680?r=Vanessa  