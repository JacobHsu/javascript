title: Closures
---

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures

```js
var name = "hello";
(function(){
  if(typeof name === "undefined") {
    var name = "world";
    console.log("goodbye "+ name); 
  } else {
    console.log("hello "+name);
  }
})();
```

"goodbye world"

```js
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12
```

```js
// fn declaration
function add(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = add(5);
var add10 = add(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12
```

箭頭函式  
https://tylermcginnis.com/arrow-functions/
```js

function add(x) {
  return (y) => x + y;
}

const addf1 = (a,b) => a + b;

var add5 = add(5);
var add10 = add(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12
console.log(addf1(5,2)); // 7
```


傳函數 (函數即物件)  
```js

const addf1 = (a,b) => a + b;

function passFn(addf1) {
  return addf1;
}

function insideFn(x,y) {
  return addf1(x,y);
}

console.log( addf1(5,2) ); // 7
console.log( passFn(addf1(5,2)) ); // 7
console.log( insideFn(5,2) ); // 7
```




```js

// global scope
var e = 10;
function sum(a){
  return function(b,c){
      return function(d){
        // local scope
        return a + b + c + d + e;
      }
    
  }
}

console.log(sum(1)(2,3)(4)); // log 20

```

## 傳多個函數

```js
function fns(a){
  return function(b,c){
        return a + b + c;
  }
}

console.log(fns(1)(2,3)); // log 6

```


```js
function fns(f1){
  return function(b,c){
        return f1(b,c);
  }
}

const addf1 = (a,b) => a + b;
console.log(fns(addf1)(2,3)); // 5

```

https://jsbin.com/yijuyebixu/edit?js,console  
```js
function fns(f1,f2){
  return function(b,c){
        return f1(b,c)+' '+f2(b)+' '+f3(b,c);  
  }
}

const f1 = (a,b) => a + b;
const f2 = (a) => a * a;
const f3 = (a,b) => a << b; //2 左移3   00010 -> 10000   16
console.log(fns(f1,f2,f3)(2,3)); // "5 4 16"

```


https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#%3E%3E_(Sign-propagating_right_shift)




