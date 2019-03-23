title: Performance
---

## 優化原則和方向

性能優化的原則是以更好的用戶體驗為標準，具體就是實現下面的目標：  

多使用內存、緩存或者其他方法  
減少 CPU 和GPU 計算，更快展現  

優化的方向有兩個：  

減少頁面體積，提升網路加載  
> 靜態資源的壓縮合併（JS 代碼壓縮合併、CSS 代碼壓縮合併）   
靜態資源緩存（資源名稱加 MD5 戳）  
使用 CDN 讓資源加載更快  

優化頁面渲染  
> CSS 放前面，JS 放後面  
懶加載（圖片懶加載、下拉加載更多） 
DOM 查詢做緩存  
減少DOM 操作，多個操作儘量合併在一起執行（`DocumentFragment`）   
儘早執行操作（`DOMContentLoaded`）  
事件節流  
使用 SSR 後端渲染，數據直接輸出到 HTML 中，減少瀏覽器使用 JS 模板渲染頁面 HTML 的時間

## 懶加載

一開始先給為 src 賦值成一個通用的預覽圖，下拉時候再動態賦值成正式的圖片。如下，preview.png是預覽圖片，比較小，加載很快，而且很多圖片都共用這個preview.png，加載一次即可。待頁面下拉，圖片顯示出來時，再去替換src為`data-realsrc`的值。

```html
<img src="img1" src="preview.jpg" data-realsrc='abc.png'>
<script type="text/javascript">
	var img1 = document.getElementById('img1')
	img1.src= img1.getAttribute('data-realsrc')
</script>
```

另外，這裡為何要用data-開頭的屬性值？
所有 HTML 中自定義的屬性，都應該用`data-`開頭，因為`data-`開頭的屬性瀏覽器渲染的時候會忽略掉，提高渲染性能。


## DOM 查詢做緩存

```js
// 每次循環，都會查詢 DOM ，耗費性能
var i
for (i = 0; i < document.getElementsByTagName('p').length; i++) {  
}
```

```js
// 只查詢一個 DOM ，緩存在 pList 中了
var pList = document.getElementsByTagName('p')  
var i
for (i = 0; i < pList.length; i++) {
    //todo
}
```

## 合併 DOM 插入 (createDocumentFragment)  

DOM 操作是非常耗費性能的，因此插入多個標籤時，先插入 `Fragment` 然後再統一插入 DOM。

```js
var listNode = document.getElementById('list')
// 要插入 10 個 li 標籤
var frag = document.createDocumentFragment();
var x, li;
for(x = 0; x < 10; x++) {
    li = document.createElement("li");
    li.innerHTML = "List item " + x;
    frag.appendChild(li);  // 先放在 frag 中，最後一次性插入到 DOM 結構中。
}
listNode.appendChild(frag);
```
## 儘早執行操作 (DOMContentLoaded)  

```js
window.addEventListener('load', function () {
    // 頁面的全部資源加載完才會執行，包括圖片、視頻等
})
document.addEventListener('DOMContentLoaded', function () {
    // DOM 渲染完即可執行，此時圖片、視頻還可能沒有加載完
})
```

## 事件節流

例如要在文字改變時觸發一個 change 事件，通過 `keyup` 來監聽。使用節流。  
> 鍵盤事件 keydown：按下鍵盤鍵 keyup：釋放鍵盤鍵  

```js
// 輸入完觸發文字修改事件  
var textarea = document.getElementById('text')
var timeoutId
textarea.addEventListener('keyup', function () {
    if (timeoutId) {
        clearTimeout(timeoutId)
    }
    // 讓連續鍵入不要頻繁觸發 change 事件 停下才觸發  
    timeoutId = setTimeout(function () {
        // 觸發 change 事件
    }, 100)
})
```

### Rreferences

https://is.gd/0IyWU2  
https://www.jianshu.com/p/8f839f558319  