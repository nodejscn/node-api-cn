
Per the [WHATWG Encoding Standard][], the encodings supported by the
`TextDecoder` API are outlined in the tables below. For each encoding,
one or more aliases may be used.

Different Node.js build configurations support different sets of encodings.
While a very basic set of encodings is supported even on Node.js builds without
ICU enabled, support for some encodings is provided only when Node.js is built
with ICU and using the full ICU data (see [Internationalization][]).

