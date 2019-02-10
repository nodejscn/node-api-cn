<!-- YAML
added: v0.1.27
-->

* {string[]}

`process.argv` 属性返回一个数组，其中包含当启动 Node.js 进程时传入的命令行参数。 
第一个元素是 [`process.execPath`]。 
如果需要访问 `argv[0]` 的原始值，参阅 `process.argv0`。 
第二个元素将是正在执行的 JavaScript 文件的路径。 
其余元素将是任何其他命令行参数。

例如，假设 `process-args.js` 的脚本如下：

```js
// 打印 process.argv。
process.argv.forEach((val, index) => {
  console.log(`${index}: ${val}`);
});
```

启动 Node.js 进程：

```console
$ node process-args.js one two=three four
```

输出如下：

```text
0: /usr/local/bin/node
1: /Users/mjr/work/node/process-args.js
2: one
3: two=three
4: four
```

