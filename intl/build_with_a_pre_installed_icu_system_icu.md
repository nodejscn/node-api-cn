
Node.js can link against an ICU build already installed on the system. In fact,
most Linux distributions already come with ICU installed, and this option would
make it possible to reuse the same set of data used by other components in the
OS.

Functionalities that only require the ICU library itself, such as
[`String.prototype.normalize()`][] and the [WHATWG URL parser][], are fully
supported under `system-icu`. Features that require ICU locale data in
addition, such as [`Intl.DateTimeFormat`][] *may* be fully or partially
supported, depending on the completeness of the ICU data installed on the
system.

