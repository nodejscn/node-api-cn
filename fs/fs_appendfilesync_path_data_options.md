<!-- YAML
added: v0.6.7
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7831
    description: The passed `options` object will never be modified.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: The `file` parameter can be a file descriptor now.
-->

* `file` {string|Buffer|URL|number} 文件名或文件描述符
* `data` {string|Buffer}
* `options` {Object|string}
  * `encoding` {string|null} 默认为 `'utf8'`
  * `mode` {integer} 默认为 `0o666`
  * `flag` {string} 默认为 `'a'`

Synchronously append data to a file, creating the file if it does not yet
exist. `data` can be a string or a [`Buffer`][].

Example:

```js
try {
  fs.appendFileSync('message.txt', 'data to append');
  console.log('The "data to append" was appended to file!');
} catch (err) {
  /* Handle the error */
}
```

If `options` is a string, then it specifies the encoding. Example:

```js
fs.appendFileSync('message.txt', 'data to append', 'utf8');
```

The `file` may be specified as a numeric file descriptor that has been opened
for appending (using `fs.open()` or `fs.openSync()`). The file descriptor will
not be closed automatically.

```js
let fd;

try {
  fd = fs.openSync('message.txt', 'a');
  fs.appendFileSync(fd, 'data to append', 'utf8');
} catch (err) {
  /* Handle the error */
} finally {
  if (fd !== undefined)
    fs.closeSync(fd);
}
```


