<!-- YAML
added: v0.7.5
-->

The `DiffieHellmanGroup` class takes a well-known modp group as its argument but
otherwise works the same as `DiffieHellman`.

```mjs
const { createDiffieHellmanGroup } = await import('crypto');
const dh = createDiffieHellmanGroup('modp1');
```

```cjs
const { createDiffieHellmanGroup } = require('crypto');
const dh = createDiffieHellmanGroup('modp1');
```

The name (e.g. `'modp1'`) is taken from [RFC 2412][] (modp1 and 2) and
[RFC 3526][]:

```console
$ perl -ne 'print "$1\n" if /"(modp\d+)"/' src/node_crypto_groups.h
modp1  #  768 bits
modp2  # 1024 bits
modp5  # 1536 bits
modp14 # 2048 bits
modp15 # etc.
modp16
modp17
modp18
```

