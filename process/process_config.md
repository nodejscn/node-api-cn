<!-- YAML
added: v0.7.7
-->

* {Object}

`process.config` 属性返回一个Javascript对象。此对象描述了用于编译当前Node.js执行程序时涉及的配置项信息。
这与执行`./configure`脚本生成的`config.gypi`文件结果是一样的。

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

*注意*： `process.config`属性值**不是**只读的，在Node.js生态系统中已经有模块扩展，修改或完全替换了`process.config`的值。


