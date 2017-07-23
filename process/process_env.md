<!-- YAML
added: v0.1.27
-->

* {Object}

`process.env`属性返回一个包含用户环境信息的对象
See environ(7).

例如这样的对象:

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

可以修改这个对象，但是下面例子的做法是不会生效的：

```命令行修改
$ node -e 'process.env.foo = "bar"' && echo $foo
```

下面的做法会生效：

```js文件中修改
process.env.foo = 'bar';
console.log(process.env.foo);
```

在`process.env`中新增一个属性，会将属性值转换成字符串

例如:

```js
process.env.test = null;
console.log(process.env.test);
// => 'null'
process.env.test = undefined;
console.log(process.env.test);
// => 'undefined'
```

用 `delete`从`process.env`中删除一个属性

例如:

```js
process.env.TEST = 1;
delete process.env.TEST;
console.log(process.env.TEST);
// => undefined
```

在Windows系统下，环境变量是不区分大小写的

例如:

```js
process.env.TEST = 1;
console.log(process.env.test);
// => 1
```

