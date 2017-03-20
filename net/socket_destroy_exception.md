<!-- YAML
added: v0.1.90
-->

确保没有更多的I/O操作在这个socket上。只有必要的以防出错（解析错误等等）。

如果`exception`被指定，[`'error'`][]将被触发并且，任何监听此事件的监听器都会收到
`exception`为参数。
