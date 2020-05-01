<!-- YAML
added: v0.5.8
changes:
  - version:
     - v11.7.0
     - v10.16.0
    pr-url: https://github.com/nodejs/node/pull/24939
    description: This class was renamed from `Zlib` to `ZlibBase`.
-->

未被 `zlib` 模块导出。
在此进行记录，因为它是压缩器/解压缩器类的基类。

该类继承自 [`stream.Transform`]，允许 `zlib` 对象用于管道和类似的流操作中。

