<!-- YAML
added: v15.0.0
-->

* `hostname` {string}

Uses the DNS protocol to resolve `CAA` records for the `hostname`. On success,
the `Promise` is resolved with an array of objects containing available
certification authority authorization records available for the `hostname`
(e.g. `[{critical: 0, iodef: 'mailto:pki@example.com'},{critical: 128, issue:
'pki.example.com'}]`).

