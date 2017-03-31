
> Stability: 2 - Stable

The `dns` module contains functions belonging to two different categories:

1) Functions that use the underlying operating system facilities to perform
name resolution, and that do not necessarily perform any network communication.
This category contains only one function: [`dns.lookup()`][]. **Developers
looking to perform name resolution in the same way that other applications on
the same operating system behave should use [`dns.lookup()`][].**

For example, looking up `iana.org`.

```js
const dns = require('dns');

dns.lookup('nodejs.org', (err, addresses, family) => {
  console.log('addresses:', addresses);
});
// address: "192.0.43.8" family: IPv4
```

2) Functions that connect to an actual DNS server to perform name resolution,
and that _always_ use the network to perform DNS queries. This category
contains all functions in the `dns` module _except_ [`dns.lookup()`][]. These
functions do not use the same set of configuration files used by
[`dns.lookup()`][] (e.g. `/etc/hosts`). These functions should be used by
developers who do not want to use the underlying operating system's facilities
for name resolution, and instead want to _always_ perform DNS queries.

Below is an example that resolves `'archive.org'` then reverse resolves the IP
addresses that are returned.

```js
const dns = require('dns');

dns.resolve4('archive.org', (err, addresses) => {
  if (err) throw err;

  console.log(`addresses: ${JSON.stringify(addresses)}`);

  addresses.forEach((a) => {
    dns.reverse(a, (err, hostnames) => {
      if (err) {
        throw err;
      }
      console.log(`reverse for ${a}: ${JSON.stringify(hostnames)}`);
    });
  });
});
```

There are subtle consequences in choosing one over the other, please consult
the [Implementation considerations section][] for more information.

