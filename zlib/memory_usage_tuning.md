
<!--type=misc-->

来自 `zlib/zconf.h`, 修改为 node.js 的用法:

解压所需的内存是(字节为单位):

<!-- eslint-disable semi -->
```js
(1 << (windowBits + 2)) + (1 << (memLevel + 9))
```

就是: 当设置为 windowBits=15 和 memLevel = 8 时(默认值), 小的对象需要 128k 加上几千字节. 

例如, 为了将默认内存需求 256k 减少到 128k, 应该这样设置:

```js
const options = { windowBits: 14, memLevel: 7 };
```

这能实现, 然而, 通常会降低压缩水平.

压缩所需的内存是 `1 << windowBits` (字节为单位). 既是, 设置为 windowBits=15(默认值)
时, 小的对象需要 32k 加上几千字节.

这是一个大小为 `chunkSize` 单个内部输出 slab 缓冲, 默认为 16k.

`level` 的设置是影响 `zlib` 压缩速度最大因素. 更高的等级设置会得到更高的压缩
水平, 然而需要更长的时间完成. 较低的等级设置会导致较少的压缩, 但会大大加快速度.

通常来说, 更大的内存使用选项意味着 Node.js 必须减少调用 `zlib`, 因为它的每个 `write` 操作
能够处理更多的数据. 所以, 这是另外一个影响速度的因素, 代价是内存的占用.
