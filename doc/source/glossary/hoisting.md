title: 提升（[Hoisting](https://developer.mozilla.org/zh-TW/docs/Glossary/Hoisting)）
---

在執行任何程式碼前，JavaScript 會把函式宣告放進記憶體裡面，這樣做的優點是：可以在程式碼宣告該函式之前使用它。

```js
function catName(name) {
  console.log("My cat's name is " + name);
}

catName("Tigger");
/*
上面程式的結果是: "My cat's name is Tigger"
*/
```

```js
console.log(c);
var c;
function c(a) {
    console.log(a);
    var a = 3;
    function a(){
    }
}
c(2);
```

// 输出 
```js
// console.log(c);
function c(a){
    console.log(a);
    var a = 3;
    function a(){
    }
}
// console.log(a);
function a(){
}
```

變量提升也有優先級, **函數聲明 > arguments > 變量聲明**

```js
var c = 1;
console.log(c);
c(2);
```

1
"TypeError: c is not a function

由於函數聲明會提升,當函數外的`console.log(c)`執行時,c已經被賦值為1。
因此,執行c(2)時會拋出TypeError,因為`1`不是函數。


---

```js
var name = 'erdong';
(function () {
    if (typeof name === 'undefined') {
        var name = 'chen';
        console.log(name);
    } else {
        console.log(name);
    }
})();
```

chen

自執行函數執行時,會先進行變量提升(這裡涉及到執行上下文不過多說,一定要搞懂執行上下文),
在自執行函數執行時,偽代碼為:

```js
(function () {
    var name;  // 變量name會提升到當前作用域頂部
    if (typeof name === 'undefined') {
        name = 'chen';
        console.log(name);
    } else {
        console.log(name);
    }
})();
```

所以會執行if中的console.log(name)