
`readline` 的一个常见用例是每次一行地输入文件。 
最简单的方法是利用 [`fs.ReadStream`] API 以及 `for await...of` 循环：

```js
const fs = require('fs');
const readline = require('readline');

async function processLineByLine() {
  const fileStream = fs.createReadStream('input.txt');

  const rl = readline.createInterface({
    input: fileStream,
    crlfDelay: Infinity
  });
  // 注意：我们使用 crlfDelay 选项将 input.txt 中的所有 CR LF 实例（'\r\n'）识别为单个换行符。

  for await (const line of rl) {
    // input.txt 中的每一行在这里将会被连续地用作 `line`。
    console.log(`Line from file: ${line}`);
  }
}

processLineByLine();
```

或者，可以使用 [`'line'`] 事件：

```js
const fs = require('fs');
const readline = require('readline');

const rl = readline.createInterface({
  input: fs.createReadStream('sample.txt'),
  crlfDelay: Infinity
});

rl.on('line', (line) => {
  console.log(`文件中的每一行: ${line}`);
});
```

目前，`for await...of` 循环可能会慢一点。 
如果 `async` / `await` 流和速度都是必不可少的，可以应用混合方法：

```js
const { once } = require('events');
const { createReadStream } = require('fs');
const { createInterface } = require('readline');

(async function processLineByLine() {
  try {
    const rl = createInterface({
      input: createReadStream('big-file.txt'),
      crlfDelay: Infinity
    });

    rl.on('line', (line) => {
      // 处理行。
    });

    await once(rl, 'close');

    console.log('文件已处理');
  } catch (err) {
    console.error(err);
  }
})();
```

