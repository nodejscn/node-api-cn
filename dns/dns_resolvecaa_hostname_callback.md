<!-- YAML
added: v15.0.0
-->

* `hostname` {string}
* `callback` {Function}
  * `err` {Error}
  * `records` {Object[]}

Uses the DNS protocol to resolve `CAA` records for the `hostname`. The
`addresses` argument passed to the `callback` function
will contain an array of certification authority authorization records
available for the `hostname` (e.g. `[{critical: 0, iodef:
'mailto:pki@example.com'}, {critical: 128, issue: 'pki.example.com'}]`).

