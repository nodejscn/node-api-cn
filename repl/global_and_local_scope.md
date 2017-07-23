
默认的解释器提供了获取存在于全局作用域中的任何变量的途径。
可以通过给每个 `REPLServer` 绑定的 `context` 对象指定变量，来显式地把变量暴露给 REPL。
例如：

```js
const repl = require('repl');
const msg = 'message';

repl.start('> ').context.m = msg;
```

`context` 对象的属性表现为 REPL 中的局部变量：

<!-- eslint-skip -->
```js
$ node repl_test.js
> m
'message'
```

注意，默认情况下 `context` 的属性不是只读的。
要指定只读的全局变量，`context` 的属性必须使用 `Object.defineProperty()` 来定义:

```js
const repl = require('repl');
const msg = 'message';

const r = repl.start('> ');
Object.defineProperty(r.context, 'm', {
  configurable: false,
  enumerable: true,
  value: msg
});
```

