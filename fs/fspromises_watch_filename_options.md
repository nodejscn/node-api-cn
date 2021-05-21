<!-- YAML
added: v15.9.0
-->

* `filename` {string|Buffer|URL}
* `options` {string|Object}
  * `persistent` {boolean} Indicates whether the process should continue to run
    as long as files are being watched. **Default:** `true`.
  * `recursive` {boolean} Indicates whether all subdirectories should be
    watched, or only the current directory. This applies when a directory is
    specified, and only on supported platforms (See [caveats][]). **Default:**
    `false`.
  * `encoding` {string} Specifies the character encoding to be used for the
     filename passed to the listener. **Default:** `'utf8'`.
  * `signal` {AbortSignal} An {AbortSignal} used to signal when the watcher
    should stop.
* Returns: {AsyncIterator} of objects with the properties:
  * `eventType` {string} The type of change
  * `filename` {string|Buffer} The name of the file changed.

Returns an async iterator that watches for changes on `filename`, where `filename`
is either a file or a directory.

```js
const { watch } = require('fs/promises');

const ac = new AbortController();
const { signal } = ac;
setTimeout(() => ac.abort(), 10000);

(async () => {
  try {
    const watcher = watch(__filename, { signal });
    for await (const event of watcher)
      console.log(event);
  } catch (err) {
    if (err.name === 'AbortError')
      return;
    throw err;
  }
})();
```

On most platforms, `'rename'` is emitted whenever a filename appears or
disappears in the directory.

All the [caveats][] for `fs.watch()` also apply to `fsPromises.watch()`.

