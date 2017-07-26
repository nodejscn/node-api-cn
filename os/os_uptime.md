<!-- YAML
added: v0.3.3
-->

* Returns: {integer}

`os.uptime()` 方法在几秒内返回操作系统的上线时间.

*注意*: 在Windows操作系统上，返回值包含了不足一秒的部分.
使用 `Math.floor()` 可以得到整数部分的上线时间（单位是秒）.
