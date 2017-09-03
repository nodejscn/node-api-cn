
* `input` {ArrayBuffer|DataView|TypedArray} An `ArrayBuffer`, `DataView` or
  Typed Array instance containing the encoded data.
* `options` {Object}
  * `stream` {boolean} `true` if additional chunks of data are expected.
    Defaults to `false`.
* Returns: {string}

Decodes the `input` and returns a string. If `options.stream` is `true`, any
incomplete byte sequences occuring at the end of the `input` are buffered
internally and emitted after the next call to `textDecoder.decode()`.

If `textDecoder.fatal` is `true`, decoding errors that occur will result in a
`TypeError` being thrown.

