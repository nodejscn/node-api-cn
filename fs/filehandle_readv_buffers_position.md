<!-- YAML
added: v14.0.0
-->

* `buffers` {ArrayBufferView[]}
* `position` {integer}
* Returns: {Promise}

Read from a file and write to an array of `ArrayBufferView`s

The `Promise` is resolved with an object containing a `bytesRead` property
identifying the number of bytes read, and a `buffers` property containing
a reference to the `buffers` input.

`position` is the offset from the beginning of the file where this data
should be read from. If `typeof position !== 'number'`, the data will be read
from the current position.

