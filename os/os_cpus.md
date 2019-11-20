<!-- YAML
added: v0.3.3
-->

* 返回: {Object[]}

返回一个对象数组，其中包含有关每个逻辑 CPU 内核的信息。

每个对象上包含的属性有：

* `model` {string}
* `speed` {number} 以兆赫兹为单位。
* `times` {Object}
  * `user` {number} CPU 在用户模式下花费的毫秒数。
  * `nice` {number} CPU 在良好模式下花费的毫秒数。
  * `sys` {number} CPU 在系统模式下花费的毫秒数。
  * `idle` {number} CPU 在空闲模式下花费的毫秒数。
  * `irq` {number} CPU 在中断请求模式下花费的毫秒数。

<!-- eslint-disable semi -->
```js
[
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 252020,
      nice: 0,
      sys: 30340,
      idle: 1070356870,
      irq: 0
    }
  },
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 306960,
      nice: 0,
      sys: 26980,
      idle: 1071569080,
      irq: 0
    }
  },
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 248450,
      nice: 0,
      sys: 21750,
      idle: 1070919370,
      irq: 0
    }
  },
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 256880,
      nice: 0,
      sys: 19430,
      idle: 1070905480,
      irq: 20
    }
  }
]
```

`nice` 的值仅适用于 POSIX。
在 Windows 上，所有处理器的 `nice` 值始终为 0。

