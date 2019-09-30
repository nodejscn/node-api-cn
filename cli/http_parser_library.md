<!-- YAML
added: v11.4.0
-->

Chooses an HTTP parser library. Available values are:

* `llhttp` for https://llhttp.org/
* `legacy` for https://github.com/nodejs/http-parser

The default is `llhttp`, unless otherwise specified when building Node.js.

This flag exists to aid in experimentation with the internal implementation of
the Node.js http parser.
This flag is likely to become a no-op and removed at some point in the future.

