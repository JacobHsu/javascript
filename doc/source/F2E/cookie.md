title: Cookie
---
因為HTTP 本身是`無狀態(Stateless)`的協議。  

無論是客戶端還是服務器端，每一次的請求都是獨立性質，而且沒有必要紀錄彼此過去的互動行為，自然而然他沒辦法記憶你每次請求的內容。 

舉凡像是登入來說，過去我們總是必須藉著不斷又不斷的登打帳號密碼，來完成網站上身分驗證的這件事情，起因當然是因為HTTP的無狀態(stateless)通訊協議造成的，而`Cookie`就是用來繞開HTTP的無狀態性的「額外手段」之一，讓伺服器可以設定或讀取Cookies中所包含資訊，藉此來維護我們在使用服務時，可以在背景完成向伺服器發送請求，接著伺服器就匯回傳包含登入憑據（使用者名稱加密碼的某種加密形式）的Cookie文檔，到使用者的硬碟(或記憶體上)，在之後登入時，只要Cookie尚未到期，瀏覽器會傳送該Cookie給伺服器作驗證憑據，來減少重複登入的輸入行為。  


## 什麼是 Cookie？

`Cookie` 是您訪問過的網站創建的文件，用於存儲瀏覽信息，例如您的網站偏好設置或個人資料信息。

共有兩種類型的 Cookie：
第一方 Cookie 是由地址欄中列出的網站域設置的 Cookie，  
而第三方 Cookie 來自在網頁上嵌入廣告或圖片等項的其他域來源。  

Cookie可以用來提升用戶體驗，比如網站可以使用Cookie來記錄用戶的登錄狀態，用戶只要登錄一次就可以不用登錄了，購物網站通過Cookie來保存購物車中的商品等。同時很多的網站分析都是依靠Cookie來完成的。

## 第一方Cookie和第三方Cookie區別


第一方 Cookie 是**設定在您目前造訪之網域中**的 Cookie。例如，如果您在 www.adobe.com/tw 中，使用第一方 Cookie 時，Cookie 會設定在 adobe.com 網域中。

第三方 Cookie 是**設定在目前造訪網域以外的**其他網域中的 Cookie。例如，如果您造訪 www.adobe.com 且 Cookie 設定在 omtrdc.com 網域中，這便是第三方 Cookie。


Cookie是必須的，離開Cookie我們什麼也分析不了。  
第一方Cookie接受率高，更準確，沒有特殊需要就用他。  
第三方Cookie可以跨域跟蹤，特別需求可以應用。  


### 第三方Cookie

這種 Cookie 是透過如社群網路等第三方程式安裝，主要目的為在本公司網站整合社群媒體內容，如社群插件 (Social Plugins)。


比如，訪問 www.a.com這個網站，這個網站設置了一個Cookie，這個Cookie也只能被 www.a.com 這個域下的網頁讀取，這就是第一方Cookie。

如果還是訪問 www.a.com這個網站，網頁裡有用到 www.b.com網站的一張圖片，瀏覽器在 www.b.com請求圖片的時候，www.b.com 設置了一個Cookie，那這個Cookie只能被 www.b.com這個域訪問，反而不能被 www.a.com 這個域訪問，

因為對我們來說，我們實際是在訪問www.a.com這個網站被設置了一個www.b.com這個域下的Cookie，所以叫第三方Cookie。

### 第三方Cookie的優勢和應用

比如，當我們有多個域名的網站需要跟蹤，我們希望瞭解到用戶點擊某個廣告到達域名A下的網頁，然後可能瀏覽了不論那個域名下的頁面，最後在域名B下的網頁完成註冊的情況。廣告可以在域名A下的網頁被跟蹤到，而註冊可以在域名B下的網頁跟蹤到。

如果我們使用第一方Cookie，會為域名A建立一個Cookie，為域名B再建立一個Cookie，他們可以關聯各自域名下網頁上的行為，但是無法關聯起來。

而使用第三方Cookie，那麼無論多少個域，都只有一個Cookie，一個屬於第三方域的Cookie，網站下所有域都能共享這個Cookie，那麼所有的行為都能被關聯起來分析。

缺點 網頁第三方 Cookies（Third-Party Cookies）會洩漏網頁瀏覽的隱私 


### Session又是什麼呢?

Cookie就像**取餐的號碼牌，認號不認人**，如果今天遺失或是被別人幹走，那你的餐點就會被其他人給領走，更別提關閉瀏覽器之後Cookie就會有被清除的風險了。

Session有點類似會話的概念，Session機制是一種服務器端的機制。  
是一種持久網路協定，讓Client端與Server端可以作一種對話，並將兩端建立關連，保持伺服器與Client可以持續的與Server作交談。  

它表示了「面向、連接」和/或「保持狀態」這樣兩個異議  
「面向、連接」表是客戶端和Server端通信前要先建立一個通信的渠道  
「保持狀態」，則是指通信交談的其中一方，可以所有的消息作關聯，就像是巷口的早餐店阿姨，還記得你最愛吃的火腿蛋不喜歡有美乃滋。

所以我們可以想像**Cookie是一張領餐的號碼牌，而Session可以是一張數位會員卡**，不僅可以記錄你的點餐號碼，還可以記憶你的餐點細節，消費記錄和點餐喜好...等。而這就解決號碼牌遺失領不到餐的問題，但是他不是記憶你帥氣得穿搭或長像，而是靠著所謂的Session ID。 


當我們需要為某個客戶端的請求創建一個Session的時候，服務器首先檢查這個客戶端的請求裡是否有包含了Session標識，就是剛剛提到的 Session id，當然如果已包含一個Session id，就表示這個客戶是老司機啦，當然伺服器端以前就為了這個客戶端創建過Session，服務器就按照Session id，把這個Session找出來使用。但如果客戶端請求不包含Session id，，則表示他是新臉孔，那伺服器端就為此客戶端創建一個Session，並生成一個Session id，並在本次響應中返回給客戶端保存。

但是在最初的 Session 設計中，我們都會把資料記錄在 Server端 上，如 Database、記憶體或是利用檔案交換的方式，來把你的點餐資訊作儲存，而當你去領飲料時，店員會輸入你的號碼，並在叫出你點的內容。但如果是大型網站上，如果有負載平衡的機制，你怎麼能確定你當初輸入和最後取餐的Server是同一台呢，而這樣作當你資料量大時，也會有效能影響的問題，這時候Cookie就出場了。


`保存這個Session id的方式也可以採用Cookie`，但似乎很多人都有一種彷彿瀏覽器關掉Session也會消失的錯覺，但本質上並非如此，就像會員卡，除非你主動提出銷卡，否則店家不會刪除顧客資料，這件事情對Session來說也如出一轍，除非通知Server刪除Session，否則Server端會一直保留來保持會話暢通，但瀏覽器從來不會主動在關閉前通知服務器要關閉
> 大部分Session機制都使用會話Cookie來保存Session ID  
而關閉瀏覽器後因為Cookie消失造成 Session id也消失了，但只要把原來的Session ID再發送給Server，那還是能夠找到原來的Session 。


但大家都會擔心，Cookie和Session得結合，到底還會不會有被竄改的問題，這個時候就要靠"簽章"來驗證資料的真實性，在我使用Cookie請求時，可以加一個簽章，也就是在我傳輸的資料後面加上一個對應的秘密字串，當伺服器回傳時，可以回應該字串，若是其他使用者偷偷串改的話，由於串改的資料和我的秘密字串無法相符，當然也無法作偽造，這就是所謂的 `SignedCookie`  
>  但記住Session就像是你的會員卡號，不見也表示仍然有資料被竊取的風險。  

如果單就實現功能，Cookie與Session彼此之間是可以互換的(指的是你可以把資料存放在Session或是Cookie，並不是指Session可以被放在Client端當Cookie使用)。但是Cookie在最單純的情況裡，是有安全性的問題(資料在Client端)。所以考量到這點，大部分都會選擇Session。但是正如Cookie是一個外加的功能，Session也不屬於HTTP協定。只要是外加功能，就必須額外寫程式實現。

不過現在做網站我們都流行使用框架，Session的機制都被框架所實現了，以Ruby on Rails來說，
> 預設的Session實現方式是由Cookie來實作的(利用加密與設定過期時間)。
每個框架實現的邏輯都可能不一樣，所以還是要去看官方的說明會比較清楚。
但從這裡可得知，Session並不是一個很明確實體的機制，算是一個概念，只要符合概念所實作出來的功能都可以被叫做Session。


#### references    
[第一方Cookie和第三方Cookie區別](https://www.biaodianfu.com/first-party-cookie-and-third-party-cookie.html)  
[判斷您是使用第一方還是第三方 Cookie](https://marketing.adobe.com/resources/help/zh_TW/whitepapers/rdc/t_cookies.html)
[五分鐘概述網路界的記憶大神-Session](https://progressbar.tw/posts/92)  