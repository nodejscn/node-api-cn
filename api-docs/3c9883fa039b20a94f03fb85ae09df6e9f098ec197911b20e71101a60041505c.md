
The [WHATWG URL Standard][] considers a handful of URL protocol schemes to be
_special_ in terms of how they are parsed and serialized. When a URL is
parsed using one of these special protocols, the `url.protocol` property
may be changed to another special protocol but cannot be changed to a
non-special protocol, and vice versa.

For instance, changing from `http` to `https` works:

```js
const u = new URL('http://example.org');
u.protocol = 'https';
console.log(u.href);
// https://example.org
```

However, changing from `http` to a hypothetical `fish` protocol does not
because the new protocol is not special.

```js
const u = new URL('http://example.org');
u.protocol = 'fish';
console.log(u.href);
// http://example.org
```

Likewise, changing from a non-special protocol to a special protocol is also
not permitted:

```js
const u = new URL('fish://example.org');
u.protocol = 'http';
console.log(u.href);
// fish://example.org
```

The protocol schemes considered to be special by the WHATWG URL Standard
include: `ftp`, `file`, `gopher`, `http`, `https`, `ws`, and `wss`.

