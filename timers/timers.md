
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

`timer` 模块开放了一个全局的 API，用于安排函数在未来某个时间点被调用。 
因为定时器函数是全局的，所以使用 API 不需要调用 `require('timers')`。

Node.js 中的定时器函数实现了与 Web 浏览器提供的定时器 API 类似的 API，但是使用了不同的内部实现（构建于 Node.js [事件循环][Event Loop]）。


