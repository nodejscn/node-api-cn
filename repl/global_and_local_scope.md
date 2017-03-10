
默认的解释器提供了获取所有全局存在的变量的途径。
可以通过给每个 `REPLServer` 绑定的 `context` 对象指定变量，来显式地把变量暴露给 REPL。
举例如下：

```js
const repl = require('repl');
var msg = 'message';

repl.start('> ').context.m = msg;
```

`context` 对象的属性表现为 REPL 中的本地变量：

```js
$ node repl_test.js
> m
'message'
```

需要注意，默认情况下 `context` 的属性*不是*只读的。
如要指定只读的全局变量，`context` 属性必须使用 `Object.defineProperty()`:

```js
const repl = require('repl');
var msg = 'message';

const r = repl.start('> ');
Object.defineProperty(r.context, 'm', {
  configurable: false,
  enumerable: true,
  value: msg
});
```

