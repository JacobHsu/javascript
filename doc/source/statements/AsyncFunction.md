title: AsyncFunction
---

async function 宣告被定義為一個回傳 AsyncFunction 物件的非同步函式 。
> 同一個步道(同步 接力賽跑 等) vs 不同步道(非同步 賽跑)

```js
let a = 0
let fn = async () => {
    a = a + await 10;
    console.log('異步')
    console.log(a)
}
fn()
console.log(++a)
```

[babeljs](https://babeljs.io/repl#?browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=DYUwLgBAhhC8EAYBQpIDMB2doGcCeGAxhABQCUcAfBAN5IQPTYwDU0A7lAJaQCMCAbnqNCAeww5RoAHTBRAcxIByQA6ugU2slZYQzESpIWQpJQtAXySZySXZJlzFLFiaA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=module&lineWrap=true&presets=es2015&prettier=false&targets=&version=7.10.0&externalPlugins=)

1 '異步' 10 
`a = await 10 + a;` 1 '異步' 11 

