# export

date.js

```js
export function formatData(data, fmt) {
    if(/(y+)/.test(fmt)) {
        fmt = fmt.replace(RegExp.$1, (data.getFullYear()+'').substr(4-RegExp.$1.length))
    }
}
// return formDate(date, 'yyyy-MM-dd hh:mm')
```

control.js

```js
export default {

}
```

com.vue

```js
import {formatData} from 'common/js/date'
// import {formatData, funB} from 'common/js/date'
import control from 'components/control'
```

