# 型変換
## Number -> String
```
let num = 100;
let s = String(100);
```

## String -> Number
```
let str = '100';
let n = Number(str);
```

# sleep
```
const sleep = (msec) => new Promise((resolve) => setTimeout(resolve, msec));
await sleep(1000);
```