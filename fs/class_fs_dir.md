<!-- YAML
added: v12.12.0
-->

代表目录流的类。

由 [`fs.opendir()`]、[`fs.opendirSync()`] 或 [`fsPromises.opendir()`] 创建。

```js
const fs = require('fs');

async function print(path) {
  const dir = await fs.promises.opendir(path);
  for await (const dirent of dir) {
    console.log(dirent.name);
  }
}
print('./').catch(console.error);
```

