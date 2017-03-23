<!-- YAML
added: v0.1.90
-->

Resolves a hostname (e.g. `'nodejs.org'`) into the first found A (IPv4) or
AAAA (IPv6) record. `options` can be an object or integer. If `options` is
not provided, then IPv4 and IPv6 addresses are both valid. If `options` is
an integer, then it must be `4` or `6`.

Alternatively, `options` can be an object containing these properties:

* `family` {Number} - The record family. If present, must be the integer
  `4` or `6`. If not provided, both IP v4 and v6 addresses are accepted.
* `hints`: {Number} - If present, it should be one or more of the supported
  `getaddrinfo` flags. If `hints` is not provided, then no flags are passed to
  `getaddrinfo`. Multiple flags can be passed through `hints` by bitwise
  `OR`ing their values.
  See [supported `getaddrinfo` flags][] for more information on supported
  flags.
* `all`: {Boolean} - When `true`, the callback returns all resolved addresses
  in an array, otherwise returns a single address. Defaults to `false`.

All properties are optional.

The `callback` function has arguments `(err, address, family)`. `address` is a
string representation of an IPv4 or IPv6 address. `family` is either the
integer `4` or `6` and denotes the family of `address` (not necessarily the
value initially passed to `lookup`).

With the `all` option set to `true`, the arguments change to
`(err, addresses)`, with `addresses` being an array of objects with the
properties `address` and `family`.

On error, `err` is an [`Error`][] object, where `err.code` is the error code.
Keep in mind that `err.code` will be set to `'ENOENT'` not only when
the hostname does not exist but also when the lookup fails in other ways
such as no available file descriptors.

`dns.lookup()` does not necessarily have anything to do with the DNS protocol.
The implementation uses an operating system facility that can associate names
with addresses, and vice versa. This implementation can have subtle but
important consequences on the behavior of any Node.js program. Please take some
time to consult the [Implementation considerations section][] before using
`dns.lookup()`.

Example usage:

```js
const dns = require('dns');
const options = {
  family: 6,
  hints: dns.ADDRCONFIG | dns.V4MAPPED,
};
dns.lookup('example.com', options, (err, address, family) =>
  console.log('address: %j family: IPv%s', address, family));
// address: "2606:2800:220:1:248:1893:25c8:1946" family: IPv6

// When options.all is true, the result will be an Array.
options.all = true;
dns.lookup('example.com', options, (err, addresses) =>
  console.log('addresses: %j', addresses));
// addresses: [{"address":"2606:2800:220:1:248:1893:25c8:1946","family":6}]
```

