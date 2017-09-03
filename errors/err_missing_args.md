
Used when a required argument of a Node.js API is not passed. This is currently
only used in the [WHATWG URL API][] for strict compliance with the specification
(which in some cases may accept `func(undefined)` but not `func()`). In most
native Node.js APIs, `func(undefined)` and `func()` are treated identically, and
the [`ERR_INVALID_ARG_TYPE`][] error code may be used instead.

<a id="ERR_NO_ICU"></a>
