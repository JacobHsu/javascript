title: factory function
---

當一個函數返回一個對象時，我們稱之他為 **工廠函數(factory function)**

```js
function createJelly() {
  return {
    type: 'jelly',
    colour: 'red'
    scoops: 3
  };
}
```

每次我們調用這個工廠函數，它將返回一個新的 jelly（果凍） 對象實例。

要注意的重點是，我們不必在工廠函數名稱前面加上create，但它可以讓其他人更清楚函數的意圖。
對於type屬性也是如此，但通常它可以幫助我們區分我們程序的對象。

### 帶參數的工廠函數

通過參數來定義我們的工廠函數 （icecream 冰淇淋），這可以用來改變返回對象的模型。

```js
function createIceCream(flavour='Vanilla') {
  return {
    type: 'icecream',
    scoops: 3,
    flavour
  }
}
```

## 組合的工廠函數

在一個工廠函數中定義另一個工廠函數，可以幫助我們把複雜的工廠函數拆分成更小的，可重用的碎片。

例如，我們可以創建一個 dessert（甜點）工廠函數，通過前面的 jelly（果凍）和 icecream（冰淇淋）工廠函數來定義。

```js
function createDessert() {
  return {
    type: 'dessert',
    bowl: [
      createJelly(),
      createIceCream()
    ]
  };
}
```

對象可以用 `has-a(具有)` 關係而不是 `is-a(是)` 來表示。也就是說，可以用組合而不是繼承來實現。

例如，使用繼承。

```js
// A trifle *is a* dessert 蛋糕*是*甜點
 
function Trifle() {
  Dessert.apply(this, arguments);
}
 
Trifle.prototype = Dessert.prototype;
 
// 或者
 
class Trifle extends Dessert {
  constructor() {
    super();
  }
}
```

我們可以用組合模式表達相同的意思。

```js
// A trifle *has* layers of jelly, custard and cream. It also *has a* topping.
// 蛋糕 *有* 果凍層，奶酪層和奶油層，頂部還 *有* 裝飾配料。
 
function createTrifle() {
  return {
    type: 'trifle',
    layers: [
      createJelly(),
      createCustard(),
      createCream()
    ],
    topping: createAlmonds()
  };
}
```

### 異步的工廠函數


並非所有工廠都會立即返回數據。例如，有些必須先獲取數據。
在這些情況下，我們可以返回 `Promises` 來定義工廠函數。

```js
function getMeal(menuUrl) {
  return new Promise((resolve, reject) => {
    fetch(menuUrl)
      .then(result => {
        resolve({
          type: 'meal',
          courses: result.json()
        });
      })
      .catch(reject);
  });
}
```

這種深度嵌套的縮進會使異步工廠難以閱讀和測試。
將它們分解成多個不同的工廠通常是有幫助的，可以使用如下編寫。

```js
function getMeal(menuUrl) {
  return fetch(menuUrl)
    .then(result => result.json())
    .then(json => createMeal(json));
}
 
function createMeal(courses=[]) {
  return {
    type: 'meal',
    courses
  };
}
```

當然，我們可以使用回調函數，但是我們已經有了 `Promise.all` 這樣的工具返回 Promises 來定義工廠函數。

```js
function getWeeksMeals() {
  const menuUrl = 'jsfood.com/';
 
  return Promise.all([
    getMeal(`${menuUrl}/monday`),
    getMeal(`${menuUrl}/tuesday`),
    getMeal(`${menuUrl}/wednesday`),
    getMeal(`${menuUrl}/thursday`),
    getMeal(`${menuUrl}/friday`)
  ]);
}
```

我們使用`get`而不是`create`作為命名約定來顯示這些工廠做一些異步工作和返回promise。

到目前為止，我們還沒有看到任何工廠用方法返回對象，這是故意的。
這是因為一般來說，我們不需要這麼做。

工廠允許我們從計算中分離我們的數據。

這意味著我們總是能夠將對象序列化為JSON，這對於在會話之間持久化，通過HTTP或WebSockets發送它們，並將它們放入數據存儲很重要。

### 高級工廠

將工廠傳遞給高階函數，這將給我們帶來巨大的控制力。例如，我們可以使用這個概念來創建一個增強的對象。

```js
function giveTimestamp(factory) {
  return (...args) => {
    const instance = factory(...args);
    const time = Date.now();
    return { time, instance };
  };
}
 
const createOrder = giveTimestamp(function(ingredients) {
  return {
    type: 'order',
    ingredients
  };
});
```
這個增強的對象採用一個現有工廠，並將其包裝以創建返回帶有`時間戳實例`的工廠。

使用這些簡單的構建塊使得我們的代碼更加友好，這絕對是我們應該關心的事情。

工廠鼓勵我們用原始數據來模擬複雜和異步數據，原始數據具有組合的自然能力，而不強迫我們去做一些高級抽象。當我們堅持簡單時，JavaScript更甜蜜！

英文原文：https://www.sitepoint.com/factory-functions-javascript/