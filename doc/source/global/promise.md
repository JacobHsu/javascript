title: Promise
---

[Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Using_promises) 是一個表示非同步運算的最終完成或失敗的物件。  Promise 對象在異步操作後可對其完成或失敗進行回調，並展示其結果值。

以下代碼片斷是一個 Promise 的示例：100ms 後使用標準輸出流打印出 `result` 字符串。
此外請注意 `catch`，他可以用於錯誤處理。Promise 是`鏈式的`。

```js
new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("result")
  }, 100)
}).then(console.log).catch(console.error)  // result
```

### `Promise` 有哪些狀態？

Promise 對象用於表示一個異步操作的最終狀態（完成或失敗）及其返回值。他有以下幾種狀態：

`pending`：初始狀態，完成或失敗狀態的前一個狀態
`fulfilled`：操作成功完成
`rejected`：操作失敗

pending 狀態的 Promise 對象會觸發 `fulfilled/rejected` 狀態，在其狀態處理方法中可以傳入參數 / 失敗信息。
當操作成功完成時，Promise 對象的 `then` 方法就會被調用；否則就會觸發 `catch`。如：

```js
const myFirstPromise = new Promise((resolve, reject) => {
    setTimeout(function(){
        resolve("成功!"); 
    }, 250);
});

myFirstPromise.then((data) => {
    console.log("完成!" + data);
}).catch((e) => {...});
```

### Promise​.all()

[Promise​.all()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) 

```js
var p1 = Promise.resolve(3);
var p2 = 1337;
var p3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'foo');
}); 

Promise.all([p1, p2, p3]).then(values => { 
  console.log(values); // [3, 1337, "foo"] 
});
```

### examples

https://jsbin.com/zosebomeko/edit?js,console,output
```js
/* 
 *  依照 tasks 順序 console 出 a, b, c
*/

const a = callback => {
  setTimeout(() => { callback('a'); }, 500);
};

const b = callback => {
  setTimeout(() => { callback('b'); }, 200);
};

const c = callback => {
  setTimeout(() => { callback('c'); }, 300);
};

const tasks = [a, b, c];

const doByOrder = (tasks, callback) => {
  // implement here
   tasks = tasks.map(function(task) {
        return new Promise((resolve, reject) => {
            task(resolve);
        });
    });
    const ansArr = [];
    let t = tasks[0];
    for (let i = 0; i < tasks.length; ++i) {
        t = t.then(p => {
            ansArr.push(p);
            //等待所有setTimeout callback function執行完畢才執行
            if (i === tasks.length - 1) {
                return callback(ansArr);
            }

            return tasks[i + 1]; //tasks[1] tasks[2] 
        });
    }
};

doByOrder(tasks, console.log.bind(console)); // expect to be ["a", "b", "c"]
```

<iframe height="480px" width="100%" src="https://repl.it/@JacobHsu/Promise1?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

<iframe height="560px" width="100%" src="https://repl.it/@JacobHsu/Promise2?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

事件循環：javascript的執行規則裡面有個`事件循環Event Loot`的規則
在事件循環中，異步事件會放到異步隊列裡面，  
但是異步隊列裡面又分為宏任務和微任務，  

瀏覽器端的  
宏任務一般有：`script標籤,setTimeout,setInterval,setImmediate,requestAnimationFrame`  
微任務有：`MutationObserver,Promise.then catch finally`  

宏任務會阻塞瀏覽器的渲染進程，微任務會在宏任務結束後立即執行，在渲染之前。

<iframe height="1280px" width="100%" src="https://repl.it/@JacobHsu/Promise3?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>


在不使用`async/await`的情況下，順序執行一組異步代碼函數，並輸出最後的結果。

<iframe height="1400px" width="100%" src="https://repl.it/@JacobHsu/Promise4?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

[Promise.race()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)

<iframe height="1500px" width="100%" src="https://repl.it/@JacobHsu/Promise5?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

### References

[把setTimeout包裝成Promise、等待所有setTimout的callback function執行完程式流程才往下執行](https://dotblogs.com.tw/shadow/2017/11/17/112535)
[promise經典面試題](https://juejin.im/post/5eec1552f265da02e7163449?utm_source=gold_browser_extension)