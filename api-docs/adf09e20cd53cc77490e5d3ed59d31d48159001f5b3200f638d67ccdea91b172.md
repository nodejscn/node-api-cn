<!-- YAML
added: v0.1.27
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18990
    description: Implicit conversion of variable value to string is deprecated.
-->

* {Object}

返回用户的环境信息。
参阅 environ(7)。

返回的对象类似如下：

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

可以修改这个对象，但是修改的内容不会影响到进程之外。
也就是说，下面的例子是无效的：

```console
$ node -e 'process.env.foo = "bar"' && echo $foo
```

下面的例子是有效的：

```js
process.env.foo = 'bar';
console.log(process.env.foo);
```

为 `process.env` 新增属性时会将属性的值转换成字符串。
在未来的版本中，如果属性的值不是字符串、数字或布尔值，则可能抛出错误。

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

在 Windows 上，环境变量不区分大小写。

```js
process.env.TEST = 1;
console.log(process.env.test);
// => 1
```

[`Worker`] 线程中的 `process.env` 是只读的。

