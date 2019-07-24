<!-- YAML
added: v10.7.0
-->
* `label` {string} **默认值:** `'default'`。
* `...data` {any}


对于先前通过调用 [`console.time()`] 启动的计时器，将经过时间和其他 `data` 参数打印到 `stdout`：


```js
console.time('process');
const value = expensiveProcess1(); // 返回 42
console.timeLog('process', value);
// 打印 "process: 365.227ms 42"。
doExpensiveProcess2(value);
console.timeEnd('process');
```

