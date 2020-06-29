# call、apply、bind

[Function.prototype.call()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

使用給定的this參數以及分別給定的參數來呼叫某個函數

[Function.prototype.apply()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

apply() 方法會呼叫一個以 this 的代表值和一個陣列形式的值組(或是一個 array-like object )為參數的函式。

[Function.prototype.bind()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

bind() 方法，會建立一個新函式。該函式被呼叫時，會將 this 關鍵字設為給定的參數，並在呼叫時，帶有提供之前，給定順序的參數。

## 為什麼我們需要 apply / bind / call ？

最大的原因還是因為 `this` 這個東西是**動態的**。（ PS. arguments 也是）  
拿到正確的 this ，而非一言不合就 `undefined`

## cab [ call , apply ] vs [ bind ]

* `call`、`apply`皆是回傳function執行結果
* `bind`方法回傳的是綁定 this 後的**原函數**

**箭頭函數** 多數時候一般函數無異，但是最大的差別在於 — 其 this 完全綁定在語彙上的位置，也就是說在 arrow 裡面的 this 永遠都是語意上的 this ，不管是誰呼叫他，或是被如何 bind 、 call 、 apply ，他永遠都是拿到原先作用域的 this 。

## bind

```js
class dog{
  constructor(name){
    this.name = name;
  }
  sayHello(){
    console.log('Hello I am ',this.name);
  }
  laterHello(){
    setTimeout(function(){
      console.log('(1 sec...) Hi!, I am',this.name)
    }, 1000);
  }
}
let boo = new dog('Corgi');
boo.sayHello();   // Hello I am  Corgi
boo.laterHello(); // (1 sec...) Hi!, I am undefined
```

```js
// Self — this 的替身
  laterHello() {
    var self = this;
    // 先把這邊的this(指向class內部)存起來
    setTimeout(function() {
      console.log('(1 sec...) Hi!, I am', self.name);
      // 因為語彙上能夠引用self變數（同個塊作用域）
      // 所以拿到了self.name
    }, 1000);
  }
```

```js
// .bind(this) — Binding大法  綁定大法
 laterHello() {
    setTimeout(
      function() {
        console.log('(1 sec...) Hi!, I am', this.name);
      }.bind(this),
      1000
    );
  }
```

```js
// Arrow Function — 箭頭函數
  laterHello() {
    setTimeout(() => {
      console.log('(1 sec...) Hi!, I am', this.name);
    }, 1000);
  }
```

## References

[函數原型最實用的 3 個方法 — call、apply、bind](https://medium.com/@realdennis/javascript-聊聊call-apply-bind的差異與相似之處-2f82a4b4dd66)