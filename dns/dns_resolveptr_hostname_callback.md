<!-- YAML
added: v6.0.0
-->
- `hostname` {string}
- `callback` {Function}
  - `err` {Error}
  - `addresses` {string[]}

Uses the DNS protocol to resolve pointer records (`PTR` records) for the
`hostname`. The `addresses` argument passed to the `callback` function will
be an array of strings containing the reply records.

