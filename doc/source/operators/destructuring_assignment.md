# [Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

```js
let a, b, rest;
[a, b] = [10, 20];
console.log(a); // 10
console.log(b); // 20

[a, b, ...rest] = [10, 20, 30, 40, 50];
console.log(a); // 10
console.log(b); // 20
console.log(rest); // [30, 40, 50]

({ a, b } = { a: 10, b: 20 });
console.log(a); // 10
console.log(b); // 20

({ a, b } = { a: 10, b: 20, c: 30 });
console.log(a); // 10
console.log(b); // 20

// Stage 4(finished) proposal
({a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40});
console.log(a); // 10
console.log(b); // 20
console.log(rest); // {c: 30, d: 40}
```

```js
const object = { a: 5, b: 6, c: 7  };
const picked = (({ a, c }) => ({ a, c }))(object);

console.log(picked); // { a: 5, c: 7 }

let unwrap = ({a, c}) => ({a, c});
let picked = unwrap({ a: 5, b: 6, c: 7 });
console.log(picked) // { a: 5, c: 7 }
```

```js
  let picked = ({date, close, symbol}) => ({date, close, symbol});
  const map1 = quotes.map( obj => {
    // console.log(obj)
    return picked(obj)
  });
  console.log(map1);
```

  [
    { date: 2020-05-14T04:00:00.000Z, close: 142.970001, symbol: 'vti' },
    { date: 2020-05-13T04:00:00.000Z, close: 141.449997, symbol: 'vti' }
  ]