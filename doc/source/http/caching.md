title: HTTP 緩存
---

HTTP 緩存分為 2 種，一種是強緩存，另一種是協商緩存。
主要作用是可以加快資源獲取速度，提升用戶體驗，減少網絡傳輸，緩解服務端的壓力。

這是緩存運作的一個整體流程圖：

![Alt http chching](https://imgur.com/NdIewPP.png)

## 強緩存

不需要發送請求到服務端，直接讀取瀏覽器本地緩存，在 Chrome 的 Network 中顯示的 HTTP 狀態碼是 200 ，在 Chrome 中，強緩存又分為 Disk Cache (存放在硬盤中)和 Memory Cache (存放在內存中)，存放的位置是由瀏覽器控制的。

是否強緩存由 `Expires`、`Cache-Control` 和 `Pragma` 3 個 Header 屬性共同來控制。

### Expires
Expires 的值是一個 `HTTP 日期`，在瀏覽器發起請求時，會根據系統時間和 Expires 的值進行比較，如果系統時間超過了 Expires 的值，緩存失效。由於和系統時間進行比較，所以當系統時間和服務器時間不一致的時候，會有緩存有效期不准的問題。Expires 的優先級在三個 Header 屬性中是最低的。

###  Cache-Control

Cache-Control 是 HTTP/1.1 中新增的屬性，在請求頭和響應頭中都可以使用，常用的屬性值如有：

max-age：單位是秒，緩存時間計算的方式是距離發起的時間的秒數，超過間隔的秒數緩存失效
`no-cache`：不使用強緩存，需要與服務器驗證緩存是否新鮮
`no-store`：禁止使用緩存（包括協商緩存），每次都向服務器請求最新的資源
private：專用於個人的緩存，中間代理、CDN 等不能緩存此響應
public：響應可以被中間代理、CDN 等緩存
must-revalidate：在緩存過期前可以使用，過期後必須向服務器驗證

###　驗證強緩存

本地通過 express 起一個服務來驗證強緩存的 3 個屬性，代碼如下：

```js
const express = require('express');
const app = express();
var options = { 
  etag: false, // 禁用協商緩存
  lastModified: false, // 禁用協商緩存
  setHeaders: (res, path, stat) => {
    res.set('Cache-Control', 'max-age=10'); // 強緩存超時時間為10秒
  },
};
app.use(express.static((__dirname + '/public'), options));
app.listen(3000);
```

第一次加載，頁面會向服務器請求數據，並在 Response Header 中添加 Cache-Control ，過期時間為 10 秒。
第二次加載，Date 頭屬性未更新，可以看到瀏覽器直接使用了強緩存，實際沒有發送請求。
過了 10 秒的超時時間之後，再次請求資源：
當 Pragma 和 Cache-Control 同時存在的時候，Pragma 的優先級高於 Cache-Control。

Headers > Response Headers > Cache-Control: max-age=10 / Pragma: no-cache

### Pragma

Pragma 只有一個屬性值，就是 `no-cache` ，效果和 Cache-Control 中的 no-cache 一致，不使用強緩存，需要與服務器驗證緩存是否新鮮，在 3 個頭部屬性中的優先級最高。

## 協商緩存

當瀏覽器的強緩存失效的時候或者請求頭中設置了不走強緩存，並且在請求頭中設置了If-Modified-Since 或者 If-None-Match 的時候，會將這兩個屬性值到服務端去驗證是否命中協商緩存，如果命中了協商緩存，會返回 304 狀態，加載瀏覽器緩存，並且響應頭會設置 Last-Modified 或者 ETag 屬性。

### ETag/If-None-Match

ETag/If-None-Match 的值是`一串 hash 碼`，代表的是`一個資源的標識`符，當服務端的文件變化的時候，它的 hash碼會隨之改變，通過請求頭中的 If-None-Match 和當前文件的 hash 值進行比較，如果相等則表示命中協商緩存。ETag 又有強弱校驗之分，如果 hash 碼是以 "W/" 開頭的一串字符串，說明此時協商緩存的校驗是弱校驗的，只有服務器上的文件差異（根據 ETag 計算方式來決定）達到能夠觸發 hash 值後綴變化的時候，才會真正地請求資源，否則返回 304 並加載瀏覽器緩存。

### Last-Modified/If-Modified-Since

Last-Modified/If-Modified-Since 的值代表的是`文件的最後修改時間`，第一次請求服務端會把資源的最後修改時間放到 Last-Modified 響應頭中，第二次發起請求的時候，請求頭會帶上上一次響應頭中的 Last-Modified 的時間，並放到 If-Modified-Since 請求頭屬性中，服務端根據文件最後一次修改時間和 If-Modified-Since 的值進行比較，如果相等，返回 304 ，並加載瀏覽器緩存。

###　驗證協商緩存


本地通過 express 起一個服務來驗證協商緩存，代碼如下：

```js
const express = require('express');
const app = express();
var options = { 
  etag: true, // 開啟協商緩存
  lastModified: true, // 開啟協商緩存
  setHeaders: (res, path, stat) => {
    res.set({
      'Cache-Control': 'max-age=00', // 瀏覽器不走強緩存
      'Pragma': 'no-cache', // 瀏覽器不走強緩存
    });
  },
};
app.use(express.static((__dirname + '/public'), options));
app.listen(3001);
```

第二次請求資源，服務端根據請求頭中的 If-Modified-Since 和 If-None-Match 驗證文件是否修改。

Tag/If-None-Match 的出現主要解決了 Last-Modified/If-Modified-Since 所解決不了的問題：

如果文件的修改頻率在秒級以下，Last-Modified/If-Modified-Since 會錯誤地返回 304
如果文件被修改了，但是內容沒有任何變化的時候，Last-Modified/If-Modified-Since 會錯誤地返回 304

## References

[HTTP caching](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Caching)
[圖解 HTTP 緩存](https://juejin.im/post/5eb7f811f265da7bbc7cc5bd?utm_source=gold_browser_extension)