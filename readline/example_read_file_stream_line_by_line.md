
例子，从一个文件系统[可读流]中每次一行地消耗输入：

```js
const readline = require('readline');
const fs = require('fs');

const rl = readline.createInterface({
  input: fs.createReadStream('sample.txt')
});

rl.on('line', (line) => {
  console.log(`文件的单行内容：${line}`);
});
```

