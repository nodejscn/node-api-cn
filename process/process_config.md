<!-- YAML
added: v0.7.7
-->

* {Object}

The `process.config` property returns an Object containing the JavaScript
representation of the configure options used to compile the current Node.js
executable. This is the same as the `config.gypi` file that was produced when
running the `./configure` script.

An example of the possible output looks like:

<!-- eslint-disable -->
```js
{
  target_defaults:
   { cflags: [],
     default_configuration: 'Release',
     defines: [],
     include_dirs: [],
     libraries: [] },
  variables:
   {
     host_arch: 'x64',
     node_install_npm: 'true',
     node_prefix: '',
     node_shared_cares: 'false',
     node_shared_http_parser: 'false',
     node_shared_libuv: 'false',
     node_shared_zlib: 'false',
     node_use_dtrace: 'false',
     node_use_openssl: 'true',
     node_shared_openssl: 'false',
     strict_aliasing: 'true',
     target_arch: 'x64',
     v8_use_snapshot: 'true'
   }
}
```

*Note*: The `process.config` property is **not** read-only and there are
existing modules in the ecosystem that are known to extend, modify, or entirely
replace the value of `process.config`.

