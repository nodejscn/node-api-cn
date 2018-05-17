<!-- YAML
added: v10.0.0
-->

* `src` {string|Buffer|URL} source filename to copy
* `dest` {string|Buffer|URL} destination filename of the copy operation
* `flags` {number} modifiers for copy operation. **Default:** `0`.
* Returns: {Promise}

Asynchronously copies `src` to `dest`. By default, `dest` is overwritten if it
already exists. The `Promise` will be resolved with no arguments upon success.

Node.js makes no guarantees about the atomicity of the copy operation. If an
error occurs after the destination file has been opened for writing, Node.js
will attempt to remove the destination.

`flags` is an optional integer that specifies the behavior
of the copy operation. It is possible to create a mask consisting of the bitwise
OR of two or more values (e.g.
`fs.constants.COPYFILE_EXCL | fs.constants.COPYFILE_FICLONE`).

* `fs.constants.COPYFILE_EXCL` - The copy operation will fail if `dest` already
exists.
* `fs.constants.COPYFILE_FICLONE` - The copy operation will attempt to create a
copy-on-write reflink. If the platform does not support copy-on-write, then a
fallback copy mechanism is used.
* `fs.constants.COPYFILE_FICLONE_FORCE` - The copy operation will attempt to
create a copy-on-write reflink. If the platform does not support copy-on-write,
then the operation will fail.

Example:

```js
const fs = require('fs');

// destination.txt will be created or overwritten by default.
fsPromises.copyFile('source.txt', 'destination.txt')
  .then(() => console.log('source.txt was copied to destination.txt'))
  .catch(() => console.log('The file could not be copied'));
```

If the third argument is a number, then it specifies `flags`, as shown in the
following example.

```js
const fs = require('fs');
const { COPYFILE_EXCL } = fs.constants;

// By using COPYFILE_EXCL, the operation will fail if destination.txt exists.
fsPromises.copyFile('source.txt', 'destination.txt', COPYFILE_EXCL)
  .then(() => console.log('source.txt was copied to destination.txt'))
  .catch(() => console.log('The file could not be copied'));
```

