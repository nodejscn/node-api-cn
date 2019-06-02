
There are equivalents to the zlib options for Brotli-based streams, although
these options have different ranges than the zlib ones:

- zlib’s `level` option matches Brotli’s `BROTLI_PARAM_QUALITY` option.
- zlib’s `windowBits` option matches Brotli’s `BROTLI_PARAM_LGWIN` option.

See [below][Brotli parameters] for more details on Brotli-specific options.

