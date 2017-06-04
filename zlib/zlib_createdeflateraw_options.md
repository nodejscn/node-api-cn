<!-- YAML
added: v0.5.8
-->

Returns a new [DeflateRaw][] object with an [options][].

*Note*: The zlib library rejects requests for 256-byte windows (i.e.,
`{ windowBits: 8 }` in `options`). An `Error` will be thrown when creating
a [DeflateRaw][] object with this specific value of the `windowBits` option.

