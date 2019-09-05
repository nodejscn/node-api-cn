<!-- YAML
added: v6.1.0
-->

* `previousValue` {Object} 上一次调用 `process.cpuUsage()` 的返回值。
* 返回: {Object}
    * `user` {integer}
    * `system` {integer}

`process.cpuUsage()` 方法返回包含当前进程的用户 CPU 时间和系统 CPU 时间的对象。
此对象包含 `user` 和 `system` 属性，属性值的单位都是微秒（百万分之一秒）。
用户和系统的属性值分别计算了执行用户程序和系统程序的时间，如果此进程在执行任务时是基于多核 CPU，值可能比实际花费的时间要大。

上一次调用 `process.cpuUsage()` 方法的结果，可以作为参数值传递给此方法，得到的结果是与上一次的差值。

```js
const startUsage = process.cpuUsage();
// { user: 38579, system: 6986 }

// 将 CPU 旋转 500 毫秒。
const now = Date.now();
while (Date.now() - now < 500);

console.log(process.cpuUsage(startUsage));
// { user: 514883, system: 11226 }
```

