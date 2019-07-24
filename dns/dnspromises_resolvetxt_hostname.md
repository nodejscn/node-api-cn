<!-- YAML
added: v10.6.0
-->
* `hostname` {string}

Uses the DNS protocol to resolve text queries (`TXT` records) for the
`hostname`. On success, the `Promise` is resolved with a two-dimensional array
of the text records available for `hostname` (e.g.
`[ ['v=spf1 ip4:0.0.0.0 ', '~all' ] ]`). Each sub-array contains TXT chunks of
one record. Depending on the use case, these could be either joined together or
treated separately.

