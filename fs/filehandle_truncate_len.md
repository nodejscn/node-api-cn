<!-- YAML
added: v10.0.0
-->
* `len` {integer} **默认值:** `0`
* 返回: {Promise}

截断文件，然后在成功时解决 `Promise` 且不带参数。

如果文件大于 `len` 个字节，则只有前面 `len` 个字节会保留在文件中。

例如，以下程序只保留文件的前 4 个字节：

```js
const fs = require('fs');
const fsPromises = fs.promises;

console.log(fs.readFileSync('temp.txt', 'utf8'));
// 打印: Node.js

async function doTruncate() {
  let filehandle = null;
  try {
    filehandle = await fsPromises.open('temp.txt', 'r+');
    await filehandle.truncate(4);
  } finally {
    if (filehandle) {
      // 如果文件已打开，则关闭文件。
      await filehandle.close();
    }
  }
  console.log(fs.readFileSync('temp.txt', 'utf8'));  // 打印: Node
}

doTruncate().catch(console.error);
```

如果文件小于 `len` 个字节，则会对其进行扩展，并且扩展部分将填充空字节（`'\0'`）：

```js
const fs = require('fs');
const fsPromises = fs.promises;

console.log(fs.readFileSync('temp.txt', 'utf8'));
// 打印: Node.js

async function doTruncate() {
  let filehandle = null;
  try {
    filehandle = await fsPromises.open('temp.txt', 'r+');
    await filehandle.truncate(10);
  } finally {
    if (filehandle) {
      // 如果文件已打开，则关闭文件。
      await filehandle.close();
    }
  }
  console.log(fs.readFileSync('temp.txt', 'utf8'));  // 打印 Node.js\0\0\0
}

doTruncate().catch(console.error);
```

最后 3 个字节是空字节（`'\0'`），以补充超出的截断。

