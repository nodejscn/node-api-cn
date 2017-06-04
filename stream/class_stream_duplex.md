<!-- YAML
added: v0.9.4
changes:
  - version: v6.8.0
    pr-url: https://github.com/nodejs/node/pull/8834
    description: Instances of `Duplex` now return `true` when
                 checking `instanceof stream.Writable`.
-->

<!--type=class-->

Duplex 流是同时实现了 [Readable][] 和
[Writable][] 接口的流。

Duplex 流的实例包括了：

* [TCP sockets][]
* [zlib streams][zlib]
* [crypto streams][crypto]

