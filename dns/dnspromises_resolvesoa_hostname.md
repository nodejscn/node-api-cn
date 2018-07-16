<!-- YAML
added: v10.6.0
-->
- `hostname` {string}

Uses the DNS protocol to resolve a start of authority record (`SOA` record) for
the `hostname`. On success, the `Promise` is resolved with an object with the
following properties:

* `nsname`
* `hostmaster`
* `serial`
* `refresh`
* `retry`
* `expire`
* `minttl`

<!-- eslint-skip -->
```js
{
  nsname: 'ns.example.com',
  hostmaster: 'root.example.com',
  serial: 2013101809,
  refresh: 10000,
  retry: 2400,
  expire: 604800,
  minttl: 3600
}
```

