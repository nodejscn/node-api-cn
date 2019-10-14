<!-- YAML
added: v12.12.0
-->

A class representing a directory stream.

Created by [`fs.opendir()`][], [`fs.opendirSync()`][], or [`fsPromises.opendir()`][].

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

