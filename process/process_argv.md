<!-- YAML
added: v0.1.27
-->

* {string[]}

返回进程启动时的命令行参数。
第一个元素是 [`process.execPath`]。
使用 `process.argv0` 可以获取 `argv[0]` 原始的值。
第二个元素是当前执行的 JavaScript 文件的路径。
剩余的元素都是额外的命令行参数。

例子，假设 `process-args.js` 文件如下:

```js
// 输出 process.argv。
process.argv.forEach((val, index) => {
  console.log(`${index}: ${val}`);
});
```

运行以下命令启动进程：

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

