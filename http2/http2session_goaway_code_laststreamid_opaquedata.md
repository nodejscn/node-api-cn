<!-- YAML
added: v9.4.0
-->

* `code` {number} An HTTP/2 error code
* `lastStreamID` {number} The numeric ID of the last processed `Http2Stream`
* `opaqueData` {Buffer|TypedArray|DataView} A `TypedArray` or `DataView`
  instance containing additional data to be carried within the `GOAWAY` frame.

Transmits a `GOAWAY` frame to the connected peer *without* shutting down the
`Http2Session`.

