<!-- YAML
added: v0.7.7
-->

* `stream` {Writable}
* `dir` {number}
  * `-1` - 光标左边
  * `1` - 光标右边
  * `0` - 整行

`readline.clearLine()` 方法会以 `dir` 指定的方向清除给定的 [TTY] 流的当前行。

