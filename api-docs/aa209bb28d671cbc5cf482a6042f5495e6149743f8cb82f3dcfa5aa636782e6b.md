
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

`readline` 模块提供了一个接口，用于一次一行地读取[可读流][Readable]（例如 [`process.stdin`]）中的数据。 
它可以使用以下方式访问：

```js
const readline = require('readline');
```

以下的简单示例说明了 `readline` 模块的基本用法。

```js
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

rl.question('你如何看待 Node.js 中文网？', (answer) => {
  // TODO：将答案记录在数据库中。
  console.log(`感谢您的宝贵意见：${answer}`);

  rl.close();
});
```

一旦调用此代码，Node.js 应用程序将不会终止，直到 `readline.Interface` 关闭，因为接口在 `input` 流上等待接收数据。



