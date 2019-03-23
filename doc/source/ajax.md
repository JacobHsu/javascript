title: AJAX
---

```js 
var xhr = new XMLHttpRequest()
xhr.open("GET","/api",false)
xhr.onreadystatechange = function () {
    // 異步執行  
    if(xhr.readyState == 4) { //響應內容解析完成，可以在客戶端調用了
        if(xhr.status == 200) { //表示成功處理請求
            alert(xhr.responseText)
        }
    }
}
xhr.send(null)
```

[XMLHttpRequest](https://developer.mozilla.org/zh-TW/docs/Web/API/XMLHttpRequest)  
[XMLHttpRequest.readyState](https://developer.mozilla.org/zh-TW/docs/Web/API/XMLHttpRequest/readyState)  
[HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)  

### 跨域

瀏覽器有同源策略，不允許ajax訪問  
跨域條件: 協議、域名、端口，有一個不同就算跨域    
所有的跨域請求都必須經由資源提供方允許  

可以跨域的三個標籤
`<img src="xxx">` `<link href="xxx">` `<script src="xxx">` 
`<link> <script>` 可以使用CDN，[CDN](https://zh.wikipedia.org/wiki/內容傳遞網路)也是其他域   



CORS是一個W3C標準，全稱是"跨域資源共享"（Cross-origin resource sharing）。

它允許瀏覽器向跨源服務器，發出XMLHttpRequest請求，從而克服了AJAX只能同源使用的限制。

CORS需要瀏覽器和服務器同時支持。實現CORS通信的關鍵是服務器。只要服務器實現了CORS接口，就可以跨源通信。


### CORS Workflow

簡單說在A網站底下若有需要去access B網站的resource  
那瀏覽器會在送去B網站的http `request的header`中加上這行   
`Origin: http://www.foo.com`
表明這個request是從www.foo.com的resource出來的

那個在B網站的web server收到了這個request後  
如果他認為A網站是B網站自己的白名單  
那麼B網站就可以在http `response`中加入這行  
`Access-Control-Allow-Origin: http://www.foo.com`
這麼一來就可以順利的拿到B網站的resource了

詳細的範例程式在
https://developer.mozilla.org/zh-TW/docs/HTTP/Access_control_CORS


[跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)  

### 異步

https://jsbin.com/hipiruzoru/edit?js,console
```js
console.log(1);
setTimeout(function(){
   console.log('setTimeout')        
},0)
let promise = new Promise(function(resolve,reject){
  console.log(3)
  resolve(100)
}).then(function(data){
  console.log(100)
})
console.log(2);

// 1 3 2 100 "setTimeout"
```

```js
console.log(0)
let promise = new Promise((resolve, reject)=>{
  console.log(1);
  setTimeout(()=>{
    console.log(2);
    resolve();
  },0)
  console.log(3)
})

promise.then(res=>{
  console.log(100)
})
console.log(4)
```
