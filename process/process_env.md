<!-- YAML
added: v0.1.27
changes:
  - version: v11.14.0
    pr-url: https://github.com/nodejs/node/pull/26544
    description: Worker threads will now use a copy of the parent thread’s
                 `process.env` by default, configurable through the `env`
                 option of the `Worker` constructor.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18990
    description: Implicit conversion of variable value to string is deprecated.
-->

* {Object}

`process.env` 属性返回包含用户环境的对象。
参阅 environ(7)。

此对象的示例如下所示：

<!-- eslint-skip -->
```js
{
  TERM: 'xterm-256color',
  SHELL: '/usr/local/bin/bash',
  USER: 'maciej',
  PATH: '~/.bin/:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin',
  PWD: '/Users/maciej',
  EDITOR: 'vim',
  SHLVL: '1',
  HOME: '/Users/maciej',
  LOGNAME: 'maciej',
  _: '/usr/local/bin/node'
}
```

可以修改此对象，但这些修改不会反映到 Node.js 进程之外，或者（除非明确请求）反映到其他 [`Worker`] 线程。
换句话说，以下示例不起作用：

```console
$ node -e 'process.env.foo = "bar"' && echo $foo
```

以下示例则起作用：

```js
process.env.foo = 'bar';
console.log(process.env.foo);
```

在 `process.env` 上分配属性将隐式地将值转换为字符串。
不推荐使用此行为。
当值不是字符串、数字或布尔值时，Node.js 的未来版本可能会抛出错误。

```js
process.env.test = null;
console.log(process.env.test);
// => 'null'
process.env.test = undefined;
console.log(process.env.test);
// => 'undefined'
```

使用 `delete` 可以从 `process.env` 中删除属性。

```js
process.env.TEST = 1;
delete process.env.TEST;
console.log(process.env.TEST);
// => undefined
```

在 Windows 操作系统上，环境变量不区分大小写。

```js
process.env.TEST = 1;
console.log(process.env.test);
// => 1
```

除非在创建 [`Worker`] 实例时明确指定，否则每个 [`Worker`] 线程都有自己的 `process.env` 副本，基于其父线程的 `process.env`，或者指定为 [`Worker`] 构造函数的 `env` 选项的任何内容。 
对于 `process.env` 的更改将在 [`Worker`] 线程中不可见，并且只有主线程可以进行对操作系统或本机加载项可见的更改。


