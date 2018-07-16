<!-- YAML
added: v10.6.0
-->
- `hostname` {string}

Uses the DNS protocol to resolve name server records (`NS` records) for the
`hostname`. On success, the `Promise` is resolved with an array of name server
records available for `hostname` (e.g.
`['ns1.example.com', 'ns2.example.com']`).

