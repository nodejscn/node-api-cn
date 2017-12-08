在使用[`script.runInThisContext()`][]或者[`vm.runInThisContext()`][]时，目标代码是在当前的V8全局对象的上下文中执行的。被传入此虚拟机上下文的目标代码会有自己独立的作用域。

要想用`http`模块搭建一个简易的服务器，被传入的代码必须要么自己执行`require('http')`，要么引用一个`http`，比如：

```js
'use strict';
const vm = require('vm');

const code = `
(function(require) {
  const http = require('http');

  http.createServer((request, response) => {
    response.writeHead(200, { 'Content-Type': 'text/plain' });
    response.end('Hello World\\n');
  }).listen(8124);

  console.log('Server running at http://127.0.0.1:8124/');
})`;

vm.runInThisContext(code)(require);
 ```

*注意*: 上述例子中的`require()`和导出它的上下文共享状态。这在运行未经认证的代码时可能会引入风险，比如在不理想的情况下修改上下文中的对象。

