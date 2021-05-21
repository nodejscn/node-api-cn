<!-- YAML
added: v15.0.0
-->
Used when an operation has been aborted (typically using an `AbortController`).

APIs _not_ using `AbortSignal`s typically do not raise an error with this code.

This code does not use the regular `ERR_*` convention Node.js errors use in
order to be compatible with the web platform's `AbortError`.

<a id="ERR_AMBIGUOUS_ARGUMENT"></a>
