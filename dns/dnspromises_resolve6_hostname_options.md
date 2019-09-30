<!-- YAML
added: v10.6.0
-->

* `hostname` {string} Hostname to resolve.
* `options` {Object}
  * `ttl` {boolean} Retrieve the Time-To-Live value (TTL) of each record.
    When `true`, the `Promise` is resolved with an array of
    `{ address: '0:1:2:3:4:5:6:7', ttl: 60 }` objects rather than an array of
    strings, with the TTL expressed in seconds.

Uses the DNS protocol to resolve IPv6 addresses (`AAAA` records) for the
`hostname`. On success, the `Promise` is resolved with an array of IPv6
addresses.

