
Node.js 自身也使用 `repl` 模块为执行 JavaScript 代码提供交互接口。
可以通过不带任何参数（或使用 `-i` 参数）地执行 Node.js 二进制文件来使用它：

<!-- eslint-skip -->
```js
$ node
> const a = [1, 2, 3];
undefined
> a
[ 1, 2, 3 ]
> a.forEach((v) => {
...   console.log(v);
...   });
1
2
3
```

