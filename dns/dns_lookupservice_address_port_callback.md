<!-- YAML
added: v0.11.14
-->
- `address` {string}
- `port` {number}
- `callback` {Function}
  - `err` {Error}
  - `hostname` {string} e.g. `example.com`
  - `service` {string} e.g. `http`

Resolves the given `address` and `port` into a hostname and service using
the operating system's underlying `getnameinfo` implementation.

If `address` is not a valid IP address, a `TypeError` will be thrown.
The `port` will be coerced to a number. If it is not a legal port, a `TypeError`
will be thrown.

On an error, `err` is an [`Error`][] object, where `err.code` is the error code.

```js
const dns = require('dns');
dns.lookupService('127.0.0.1', 22, (err, hostname, service) => {
  console.log(hostname, service);
  // Prints: localhost ssh
});
```

If this method is invoked as its [`util.promisify()`][]ed version, it returns a
Promise for an object with `hostname` and `service` properties.

