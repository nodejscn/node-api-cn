
There are several options that can be set on Brotli encoders, affecting
compression efficiency and speed. Both the keys and the values can be accessed
as properties of the `zlib.constants` object.

The most important options are:

* `BROTLI_PARAM_MODE`
  * `BROTLI_MODE_GENERIC` (default)
  * `BROTLI_MODE_TEXT`, adjusted for UTF-8 text
  * `BROTLI_MODE_FONT`, adjusted for WOFF 2.0 fonts
* `BROTLI_PARAM_QUALITY`
  * Ranges from `BROTLI_MIN_QUALITY` to `BROTLI_MAX_QUALITY`,
    with a default of `BROTLI_DEFAULT_QUALITY`.
* `BROTLI_PARAM_SIZE_HINT`
  * Integer value representing the expected input size;
    defaults to `0` for an unknown input size.

The following flags can be set for advanced control over the compression
algorithm and memory usage tuning:

* `BROTLI_PARAM_LGWIN`
  * Ranges from `BROTLI_MIN_WINDOW_BITS` to `BROTLI_MAX_WINDOW_BITS`,
    with a default of `BROTLI_DEFAULT_WINDOW`, or up to
    `BROTLI_LARGE_MAX_WINDOW_BITS` if the `BROTLI_PARAM_LARGE_WINDOW` flag
    is set.
* `BROTLI_PARAM_LGBLOCK`
  * Ranges from `BROTLI_MIN_INPUT_BLOCK_BITS` to `BROTLI_MAX_INPUT_BLOCK_BITS`.
* `BROTLI_PARAM_DISABLE_LITERAL_CONTEXT_MODELING`
  * Boolean flag that decreases compression ratio in favour of
    decompression speed.
* `BROTLI_PARAM_LARGE_WINDOW`
  * Boolean flag enabling “Large Window Brotli” mode (not compatible with the
    Brotli format as standardized in [RFC 7932][]).
* `BROTLI_PARAM_NPOSTFIX`
  * Ranges from `0` to `BROTLI_MAX_NPOSTFIX`.
* `BROTLI_PARAM_NDIRECT`
  * Ranges from `0` to `15 << NPOSTFIX` in steps of `1 << NPOSTFIX`.

