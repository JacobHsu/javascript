## map 

對元素重新組裝，生成新陣列
[Array.prototype.map()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/map)  

https://jsbin.com/xevunu/edit?js,console
```js
var arr = [1, 2, 3];
var arr2 = arr.map(function(item,index){
    return '<b>'+item+'</b>';

})
console.log(arr2);
// expected output: ["<b>1</b>", "<b>2</b>", "<b>3</b>"]
```

```js
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```


`res.map( (v,i)=>{ console.log(i,v) } )`

react-ts-epirus\src\utils\api\queries.ts

```js
 .then(postEthGetFilterLogsRes=> {
    let hashList = [], fromtoArr=[];
    postEthGetFilterLogsRes.map( v=> {
        let transactionHash = v.transactionHash;
        fromtoArr.push( { transactionHash:transactionHash })
        hashList.push(v.transactionHash)
    })

    return Promise.all(hashList.map((hash) => fetchData3(`/transactions/${hash}`)))
    .then((values) => {

    let transactionsArr = [];
    values.map( (v,i)=>{
        let timestampISO = v.timestampISO;
        let value = v.functionMeta.params.length === 0 ? 0 : v.functionMeta.params[1].value
        let add_transactionHash = fromtoArr[i].transactionHash
        transactionsArr.push( { 
            timestampISO: timestampISO, value: value,
            add_transactionHash: add_transactionHash
        } )
    })
    return transactionsArr;
    })
    .catch(() => {

    })
    .finally(() => {

    });
})
.then( res=> {

    let ans = res as any[];
    let resans = ans.map(v=> {
        const timestampISO = v.timestampISO;
        const value = v.value;
         const add_transactionHash = v.add_transactionHash;
        return {
        'timestampISO': timestampISO,
        'value': value,
        'hash': add_transactionHash,
        };
    })

    return resans;
})
```
