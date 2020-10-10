<!-- YAML
added: v0.1.27
-->

* {string[]}

`process.argv` 属性会返回一个数组，其中包含当 Node.js 进程被启动时传入的命令行参数。 
第一个元素是 [`process.execPath`]。 
如果需要访问 `argv[0]` 的原始值，则参见 `process.argv0`。 
第二个元素是正被执行的 JavaScript 文件的路径。 
其余的元素是任何额外的命令行参数。

例如，假设 `process-args.js` 的脚本如下：

```js
// 打印 process.argv。
process.argv.forEach((val, index) => {
  console.log(`${index}: ${val}`);
});
```

启动 Node.js 进程：

```console
$ node process-args.js 参数1 参数2 参数3
```

输出如下：

```text
0: /usr/local/bin/node
1: /Users/mjr/work/node/process-args.js
2: 参数1
3: 参数2
4: 参数3
```

