<!-- YAML
added: v0.7.7
-->

* {Object}

`process.config` 属性返回一个 `Object`，其中包含用于编译当前 Node.js 可执行文件的配置选项的 JavaScript 表示形式。 
这与运行 `./configure` 脚本时生成的 `config.gypi` 文件相同。

可能的输出样例:

<!-- eslint-skip -->
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
     napi_build_version: 5,
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
     v8_use_snapshot: 1
   }
}
```

`process.config` 属性值不是只读的，在 Node.js 生态系统中已经有模块扩展、修改或完全替换了 `process.config` 的值。


