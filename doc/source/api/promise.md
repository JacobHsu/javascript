# Promise

[JavaScript Promise 全介紹](https://wcc723.github.io/development/2020/02/16/all-new-promise/)

Ajax 是屬於一個透過 JavaScript 技術名稱，用於取得遠端資料；
而 Promise 則是一個語法，專門用來處理非同步行為，

透過 `new Promise()` 的方式建立 p 物件，此時 p 就能使用 `Promise` 的原型方法：

```js
const p = new Promise();

p.then();    // Promise 回傳正確
p.catch();   // Promise 回傳失敗
p.finally(); // 非同步執行完畢（無論是否正確完成）
```

狀態

`pending`：事件已經運行中，尚未取得結果  
`resolved`：事件已經執行完畢且成功操作，回傳 resolve 的結果（該承諾已經被實現 `fulfilled`）  
`rejected`：事件已經執行完畢但操作失敗，回傳 rejected 的結果  

上列的三種狀態每次執行必定會經過 Pending，
接下來進入 Fulfilled 或 Rejected 的其中之一，
並且可以使用 `then()` 及 `catch()` 取得成功或失敗的結果。


在大部分情況下，開發者習慣僅使用 .then() 來取得成功的結果，失敗的部分交由 catch(onRejected) 來處理

```js
// promise.then(onFulfilled);
// promise.catch(onRejected)
promise()
  .then(success => {
    console.log(success);
  })
// 失敗的行為一律交給了 catch
  .catch(fail => {
    console.log(fail);
  });
```

## 鏈接

Promise 另一個特點在於 then、catch 都可以使用鏈接的方式不斷的進行下一個任務

如果是 promise 函式，則會`繼續遵循 then 及 catch 的運作`
如果不是 promise 函式，在下一個 then 則可以取得結果

```js
promise(1)
  .then(success => {
    console.log(success);
    return promise(2);
  })
  .then(success => {
    console.log(success);
    return promise(0); // 這個階段會進入 catch
  })
  .then(success => {   // 由於上一個階段結果是 reject，所以此段不執行
    console.log(success);
    return promise(3);
  })
  .catch(fail => {
    console.log(fail);
  })
  .finally(() => {
    console.log('done');
  })
```

```js
const res = onPress() // 異步函數
if( res & res.then ) {
  res.then((close).catch( ()=>{}) ) //等函數調用完 調用close
} else close() //否則 立馬調用close
```
