
> 稳定性: 2 - 稳定的

`require('readline')` 模块提供了一个接口，用于从[可读流]（如 [`process.stdin`]）读取数据，每次读取一行。
它可以通过以下方式使用：

```js
const readline = require('readline');
```

例子，`readline` 模块的基本用法：

```js
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

rl.question('你认为 Node.js 中文网怎么样？', (answer) => {
  // 对答案进行处理
  console.log(`多谢你的反馈：${answer}`);

  rl.close();
});
```

注意：当调用该代码时，Node.js 程序不会终止，直到 `readline.Interface` 被关闭，因为接口在等待 `input` 流中要被接收的数据。

