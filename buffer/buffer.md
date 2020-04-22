
<!--introduced_in=v0.1.90-->

> 稳定性: 2 - 稳定

在 Node.js 中，`Buffer` 对象用于以字节序列的形式来表示二进制数据。 
许多 Node.js 的 API（例如流和文件系统操作）都支持 `Buffer`，因为与操作系统或其他进程的交互通常总是以二进制数据的形式发生。

`Buffer` 类是 JavaScript 语言内置的 [`Uint8Array`] 类的子类。 
支持许多涵盖其他用例的额外方法。 
只要支持 `Buffer` 的地方，Node.js API 都可以接受普通的 [`Uint8Array`]。

`Buffer` 类的实例，以及通常的 [`Uint8Array`]，类似于从 `0` 到 `255` 之间的整数数组，但对应于固定大小的内存块，并且不能包含任何其他值。 
一个 `Buffer` 的大小在创建时确定，且无法更改。

`Buffer` 类在全局作用域中，因此无需使用 `require('buffer').Buffer`。

```js
// 创建一个长度为 10 的 Buffer，
// 其中填充了全部值为 `1` 的字节。
const buf1 = Buffer.alloc(10);

// 创建一个长度为 10、且用 0x1 填充的 Buffer。 
const buf2 = Buffer.alloc(10, 1);

// 创建一个长度为 10、且未初始化的 Buffer。
// 这个方法比调用 Buffer.alloc() 更快，
// 但返回的 Buffer 实例可能包含旧数据，
// 因此需要使用 fill()、write() 或其他能填充 Buffer 的内容的函数进行重写。
const buf3 = Buffer.allocUnsafe(10);

// 创建一个包含字节 [1, 2, 3] 的 Buffer。
const buf4 = Buffer.from([1, 2, 3]);

// 创建一个包含字节 [1, 1, 1, 1] 的 Buffer，
// 其中所有条目均使用 `(value & 255)` 进行截断以符合 0-255 的范围。
const buf5 = Buffer.from([257, 257.5, -255, '1']);

// 创建一个 Buffer，其中包含字符串 'tést' 的 UTF-8 编码字节：
// [0x74, 0xc3, 0xa9, 0x73, 0x74]（以十六进制表示）
// [116, 195, 169, 115, 116]（以十进制表示）
const buf6 = Buffer.from('tést');

// 创建一个包含 Latin-1 字节 [0x74, 0xe9, 0x73, 0x74] 的 Buffer。
const buf7 = Buffer.from('tést', 'latin1');
```

