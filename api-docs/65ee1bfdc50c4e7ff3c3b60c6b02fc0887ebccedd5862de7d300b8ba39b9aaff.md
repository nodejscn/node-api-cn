
`readline` 的一个常见用例是每次一行地从文件系统[可读流][Readable]消费输入：

```js
const readline = require('readline');
const fs = require('fs');

const rl = readline.createInterface({
  input: fs.createReadStream('sample.txt'),
  crlfDelay: Infinity
});

rl.on('line', (line) => {
  console.log(`文件的每行内容：${line}`);
});
```

