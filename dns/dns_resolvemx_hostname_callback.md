<!-- YAML
added: v0.1.27
-->
- `hostname` {string}
- `callback` {Function}
  - `err` {Error}
  - `addresses` {Object[]}

Uses the DNS protocol to resolve mail exchange records (`MX` records) for the
`hostname`. The `addresses` argument passed to the `callback` function will
contain an array of objects containing both a `priority` and `exchange`
property (e.g. `[{priority: 10, exchange: 'mx.example.com'}, ...]`).

