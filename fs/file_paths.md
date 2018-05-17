
Most `fs` operations accept filepaths that may be specified in the form of
a string, a [`Buffer`][], or a [`URL`][] object using the `file:` protocol.

String form paths are interpreted as UTF-8 character sequences identifying
the absolute or relative filename. Relative paths will be resolved relative
to the current working directory as specified by `process.cwd()`.

Example using an absolute path on POSIX:

```js
const fs = require('fs');

fs.open('/open/some/file.txt', 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

Example using a relative path on POSIX (relative to `process.cwd()`):

```js
fs.open('file.txt', 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

Paths specified using a [`Buffer`][] are useful primarily on certain POSIX
operating systems that treat file paths as opaque byte sequences. On such
systems, it is possible for a single file path to contain sub-sequences that
use multiple character encodings. As with string paths, `Buffer` paths may
be relative or absolute:

Example using an absolute path on POSIX:

```js
fs.open(Buffer.from('/open/some/file.txt'), 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

*Note:* On Windows Node.js follows the concept of per-drive working directory.
This behavior can be observed when using a drive path without a backslash. For
example `fs.readdirSync('c:\\')` can potentially return a different result than
`fs.readdirSync('c:')`. For more information, see
[this MSDN page][MSDN-Rel-Path].

