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


取得用get傳遞之網址列資訊(Query String)  

https://jsbin.com/katifugevu/edit?js,console,output
```js
//取得網址字串
var url = location.href;
    url = 'http://example.com/?userid=jacob.hsu';
//再來用去尋找網址列中是否有資料傳遞(QueryString)
if(url.indexOf('?')!=-1)
{
    var id = "";
    //在此直接將各自的參數資料切割放進ary中
    var ary = url.split('?')[1].split('&');
    // console.log(ary); ["userid=jacob.hsu"]
    
    //下迴圈去搜尋每個資料參數
    for(i=0;i<=ary.length-1;i++)
    {
        //如果資料名稱為id的話那就把他取出來
        if(ary[i].split('=')[0] == 'userid')
            id = ary[i].split('=')[1];
            console.log(id); //"jacob.hsu"
    }
    
}
```

ref : 
https://ithelp.ithome.com.tw/articles/10190254



ex: http://blog.xuite.net/ahdaa/blog1/test.html?id=AD&val1=02&val2=22#achorAD
```js
  location.href     // 完整的網址
  location.protocol // 協定　　　　　　 http:
  location.hostname // 伺服器名稱　　　 blog.xuite.net
  location.host     // 伺服器:埠號　　　blog.xuite.net:80
  location.port     // 埠號　　　　　　 80
  location.pathname // host之後的部份  /ahdaa/blog1/test.html?id=AD&val1=02&val2=22#achorAD
  location.search   // 含?之後所有字串　?id=AD&val1=02&val2=22#achorAD
  location.hash     // 含#之後所有字串　#achorAD(通常用於錨點)
```

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
