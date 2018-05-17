<!-- YAML
added: v10.0.0
-->

* `filehandle` {FileHandle}
* `len` {integer} **Default:** `0`
* Returns: {Promise}

Truncates the file represented by `filehandle` then resolves the `Promise`
with no arguments upon success.

If the file referred to by the `FileHandle` was larger than `len` bytes, only
the first `len` bytes will be retained in the file.

For example, the following program retains only the first four bytes of the
file:

```js
console.log(fs.readFileSync('temp.txt', 'utf8'));
// Prints: Node.js

async function doTruncate() {
  const fd = await fsPromises.open('temp.txt', 'r+');
  await fsPromises.ftruncate(fd, 4);
  console.log(fs.readFileSync('temp.txt', 'utf8'));  // Prints: Node
}

doTruncate().catch(console.error);
```

If the file previously was shorter than `len` bytes, it is extended, and the
extended part is filled with null bytes (`'\0'`). For example,

```js
console.log(fs.readFileSync('temp.txt', 'utf8'));
// Prints: Node.js

async function doTruncate() {
  const fd = await fsPromises.open('temp.txt', 'r+');
  await fsPromises.ftruncate(fd, 10);
  console.log(fs.readFileSync('temp.txt', 'utf8'));  // Prints Node.js\0\0\0
}

doTruncate().catch(console.error);
```

The last three bytes are null bytes (`'\0'`), to compensate the over-truncation.

