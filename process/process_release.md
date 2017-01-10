<!-- YAML
added: v3.0.0
-->

The `process.release` property returns an Object containing metadata related to
the current release, including URLs for the source tarball and headers-only
tarball.

`process.release` contains the following properties:

* `name` {String} A value that will always be `'node'` for Node.js. For
  legacy io.js releases, this will be `'io.js'`.
* `lts`: a string with a value indicating the _codename_ of the LTS (Long-term
  Support) line the current release is part of. This property only exists for
  LTS releases and is `undefined` for all other release types, including stable
  releases. Current valid values are:
  - `"Argon"` for the v4.x LTS line beginning with v4.2.0.
  - `"Boron"` for the v6.x LTS line beginning with v6.9.0.
* `sourceUrl` {String} an absolute URL pointing to a _`.tar.gz`_ file containing
  the source code of the current release.
* `headersUrl`{String} an absolute URL pointing to a _`.tar.gz`_ file containing
  only the source header files for the current release. This file is
  significantly smaller than the full source file and can be used for compiling
  Node.js native add-ons.
* `libUrl` {String} an absolute URL pointing to a _`node.lib`_ file matching the
  architecture and version of the current release. This file is used for
  compiling Node.js native add-ons. _This property is only present on Windows
  builds of Node.js and will be missing on all other platforms._
* `lts` {String} a string label identifying the [LTS][] label for this release.
  If the Node.js release is not an LTS release, this will be `undefined`.

For example:

```js
{
  name: 'node',
  lts: 'Argon',
  sourceUrl: 'https://nodejs.org/download/release/v4.4.5/node-v4.4.5.tar.gz',
  headersUrl: 'https://nodejs.org/download/release/v4.4.5/node-v4.4.5-headers.tar.gz',
  libUrl: 'https://nodejs.org/download/release/v4.4.5/win-x64/node.lib'
}
```

In custom builds from non-release versions of the source tree, only the
`name` property may be present. The additional properties should not be
relied upon to exist.

