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

