title: JS 不良編碼習慣
---

### 不要使用早期的JavaScript技巧

它的創建者沒有料到這種語言會如此流行。

基於JavaScript構建的應用程序的複雜性比語言發展的速度還要快。這種情況迫使開發人員使用JavaScript技巧和變通方法，只是為了讓事情正常運行。

一個典型的例子是查看數組是否包含某個元素。

ES6 中可以使用 `array.includes(item)` 來代替 `array.indexOf(item) !== -1`  