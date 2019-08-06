<!-- YAML
changes:
  - version: v10.6.0
    pr-url: https://github.com/nodejs/node/pull/21498
    description: Deprecation revoked.
  - version:
    - v4.8.6
    - v6.12.0
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v0.4.7
    description: Documentation-only deprecation.
-->

Type: Deprecation revoked

The [`fs.lchown(path, uid, gid, callback)`][] API was deprecated. The
deprecation was revoked because the requisite supporting APIs were added in
libuv.

<a id="DEP0038"></a>
