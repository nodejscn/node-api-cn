<!-- YAML
added: v0.5.0
-->

* 返回: {string}

`os.arch()`方法返回一个字符串, 表明*Node.js 二进制编译* 所用的
操作系统CPU架构.

现在可能的值有: `'arm'`, `'arm64'`, `'ia32'`, `'mips'`,
`'mipsel'`, `'ppc'`, `'ppc64'`, `'s390'`, `'s390x'`, `'x32'`, `'x64'`,  和
`'x86'`.

等价于 [`process.arch`][].

