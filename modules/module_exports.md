<!-- YAML
added: v0.1.16
-->

* {Object}

`module.exports` 对象由 `Module` 系统创建。  
有时这种这种设定让开发者无法接受,因为他们很想让自己的`module` 能够直接成为某个类的实例，为了实现这种想法：    
你需要将所需的导出对象指定给`module.exports` 。     
但是将你如果将导出的对象直接分配给exports(虽然这样会看起来很方便),但可能会出现你不想要的结果(比如exports被重新赋值了)。   

例如，假设正在创建一个名为 `a.js` 的模块：

```js
const EventEmitter = require('events');

module.exports = new EventEmitter();

// 处理一些工作，并在一段时间后从模块自身触发 'ready' 事件。
setTimeout(() => {
  module.exports.emit('ready');
}, 1000);
```

然后，在另一个文件中可以这么做：

```js
const a = require('./a');
a.on('ready', () => {
  console.log('模块 a 已准备好');
});
```

对 `module.exports` 的赋值必须立即完成。
不能在任何回调中完成。
以下是不起作用的：

`x.js`:

```js
setTimeout(() => {
  module.exports = { a: 'hello' };
}, 0);
```

`y.js`:

```js
const x = require('./x');
console.log(x.a);
```

