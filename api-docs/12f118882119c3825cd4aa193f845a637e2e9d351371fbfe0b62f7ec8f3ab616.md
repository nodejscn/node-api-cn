
While calling `napi_create_typedarray()`, `(length * size_of_element) +
byte_offset` was larger than the length of given `buffer`.

<a id="ERR_NAPI_TSFN_CALL_JS"></a>
