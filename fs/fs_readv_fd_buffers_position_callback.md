<!-- YAML
added:
 - v13.13.0
 - v12.17.0
-->

* `fd` {integer}
* `buffers` {ArrayBufferView[]}
* `position` {integer}
* `callback` {Function}
  * `err` {Error}
  * `bytesRead` {integer}
  * `buffers` {ArrayBufferView[]}

Read from a file specified by `fd` and write to an array of `ArrayBufferView`s
using `readv()`.

`position` is the offset from the beginning of the file from where data
should be read. If `typeof position !== 'number'`, the data will be read
from the current position.

The callback will be given three arguments: `err`, `bytesRead`, and
`buffers`. `bytesRead` is how many bytes were read from the file.

If this method is invoked as its [`util.promisify()`][]ed version, it returns
a promise for an `Object` with `bytesRead` and `buffers` properties.

