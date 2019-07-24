<!-- YAML
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18017
    description: Runtime deprecation.
-->

Type: Runtime

Node.js supports all GCM authentication tag lengths which are accepted by
OpenSSL when calling [`decipher.setAuthTag()`][]. This behavior will change in
a future version at which point only authentication tag lengths of 128, 120,
112, 104, 96, 64, and 32 bits will be allowed. Authentication tags whose length
is not included in this list will be considered invalid in compliance with
[NIST SP 800-38D][].

<a id="DEP0091"></a>
