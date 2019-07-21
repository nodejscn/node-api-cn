<!-- YAML
added: v10.0.0
-->

* 返回: {Promise} 如果底层的文件描述符被关闭则 `Promise` 将会被解决，如果关闭时发生错误则将 `Promise` 将会被拒绝。
关闭文件描述符。

```js
const fsPromises = require('fs').promises;
async function openAndClose() {
  let filehandle;
  try {
    filehandle = await fsPromises.open('thefile.txt', 'r');
  } finally {
    if (filehandle !== undefined)
      await filehandle.close();
  }
}
```

