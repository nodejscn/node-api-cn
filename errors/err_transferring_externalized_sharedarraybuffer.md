
A `SharedArrayBuffer` whose memory is not managed by the JavaScript engine
or by Node.js was encountered during serialization. Such a `SharedArrayBuffer`
cannot be serialized.

This can only happen when native addons create `SharedArrayBuffer`s in
"externalized" mode, or put existing `SharedArrayBuffer` into externalized mode.

<a id="ERR_TRANSFORM_ALREADY_TRANSFORMING"></a>
