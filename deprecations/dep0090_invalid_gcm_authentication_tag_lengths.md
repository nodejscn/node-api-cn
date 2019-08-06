<!-- YAML
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/17825
    description: End-of-Life.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18017
    description: Runtime deprecation.
-->

Type: End-of-Life

Node.js used to support all GCM authentication tag lengths which are accepted by
OpenSSL when calling [`decipher.setAuthTag()`][]. Beginning with Node.js
v11.0.0, only authentication tag lengths of 128, 120, 112, 104, 96, 64, and 32
bits are allowed. Authentication tags of other lengths are invalid per
[NIST SP 800-38D][].

<a id="DEP0091"></a>
