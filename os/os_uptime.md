<!-- YAML
added: v0.3.3
-->

* Returns: {Integer}

`os.uptime()` 方法在几秒内返回操作系统的上线时间.

*注意*: 在 Node.js' 内部, 这个数值是用 `double` 来表示的.
然而, 小数秒数不会被返回, 因此其值通常被认为是整数.
