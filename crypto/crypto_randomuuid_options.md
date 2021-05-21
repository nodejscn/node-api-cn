<!-- YAML
added: v15.6.0
-->

* `options` {Object}
  * `disableEntropyCache` {boolean} By default, to improve performance,
    Node.js generates and caches enough
    random data to generate up to 128 random UUIDs. To generate a UUID
    without using the cache, set `disableEntropyCache` to `true`.
    **Default:** `false`.
* Returns: {string}

Generates a random [RFC 4122][] Version 4 UUID. The UUID is generated using a
cryptographic pseudorandom number generator.

