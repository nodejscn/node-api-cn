<!-- YAML
added: v10.0.0
-->

* Returns: {Promise} A `Promise` that will be resolved once the underlying
  file descriptor is closed, or will be rejected if an error occurs while
  closing.

Closes the file descriptor.

```js
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

