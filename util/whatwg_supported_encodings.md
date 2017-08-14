
Per the [WHATWG Encoding Standard][], the encodings supported by the
`TextDecoder` API are outlined in the tables below. For each encoding,
one or more aliases may be used. Support for some encodings is enabled
only when Node.js is using the full ICU data (see [Internationalization][]).
`util.TextDecoder` is `undefined` when ICU is not enabled during build.

