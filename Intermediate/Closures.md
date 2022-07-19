
# 閉包

一個函數和詞法環境的引用捆綁的組合就是閉包（「`closure`」）
閉包的作用在於可以讓子級作用域使用父級作用域的變量，同時這些變量在不同的閉包是不可見的。  
閉包（Closure）是函式以及該函式被宣告時所在的作用域環境（lexical environment）的組合。  

應用場景

模塊封裝，防止變量污染全局

```js
var Person = (function(){
  	var name = 'Jacob'
    function Person() {
      console.log('work for qtt')
    }
  Person.prototype.work = function() {}
   return Person
})()
```

循環體中創建閉包，保存變量

```js
for(var i=0;i<5;i++){
  (function(j){
      setTimeOut(() => {
        console.log(j)
      },1000)
  })(i)
}
```