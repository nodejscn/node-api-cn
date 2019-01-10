<!-- YAML
added: v10.6.0
-->
* `hostname` {string}
* `options` {integer | Object}
  - `family` {integer} The record family. Must be `4` or `6`. IPv4
    and IPv6 addresses are both returned by default.
  - `hints` {number} One or more [supported `getaddrinfo` flags][]. Multiple
    flags may be passed by bitwise `OR`ing their values.
  - `all` {boolean} When `true`, the `Promise` is resolved with all addresses in
    an array. Otherwise, returns a single address. **Default:** `false`.
  - `verbatim` {boolean} When `true`, the `Promise` is resolved with IPv4 and
    IPv6 addresses in the order the DNS resolver returned them. When `false`,
    IPv4 addresses are placed before IPv6 addresses.
    **Default:** currently `false` (addresses are reordered) but this is
    expected to change in the not too distant future.
    New code should use `{ verbatim: true }`.

Resolves a hostname (e.g. `'nodejs.org'`) into the first found A (IPv4) or
AAAA (IPv6) record. All `option` properties are optional. If `options` is an
integer, then it must be `4` or `6` – if `options` is not provided, then IPv4
and IPv6 addresses are both returned if found.

With the `all` option set to `true`, the `Promise` is resolved with `addresses`
being an array of objects with the properties `address` and `family`.

On error, the `Promise` is rejected with an [`Error`][] object, where `err.code`
is the error code.
Keep in mind that `err.code` will be set to `'ENOENT'` not only when
the hostname does not exist but also when the lookup fails in other ways
such as no available file descriptors.

[`dnsPromises.lookup()`][] does not necessarily have anything to do with the DNS
protocol. The implementation uses an operating system facility that can
associate names with addresses, and vice versa. This implementation can have
subtle but important consequences on the behavior of any Node.js program. Please
take some time to consult the [Implementation considerations section][] before
using `dnsPromises.lookup()`.

Example usage:

```js
const dns = require('dns');
const dnsPromises = dns.promises;
const options = {
  family: 6,
  hints: dns.ADDRCONFIG | dns.V4MAPPED,
};

dnsPromises.lookup('example.com', options).then((result) => {
  console.log('address: %j family: IPv%s', result.address, result.family);
  // address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6
});

// When options.all is true, the result will be an Array.
options.all = true;
dnsPromises.lookup('example.com', options).then((result) => {
  console.log('addresses: %j', result);
  // addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
});
```

