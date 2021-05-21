<!-- YAML
added:
 - v13.13.0
 - v12.17.0
-->

* `buffers` {Buffer[]|TypedArray[]|DataView[]}
* `position` {integer} The offset from the beginning of the file where the data
  should be read from. If `position` is not a `number`, the data will be read
  from the current position.
* Returns: {Promise} Fulfills upon success an object containing two properties:
  * `bytesRead` {integer} the number of bytes read
  * `buffers` {Buffer[]|TypedArray[]|DataView[]} property containing
    a reference to the `buffers` input.

Read from a file and write to an array of {ArrayBufferView}s

