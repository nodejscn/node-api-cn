<!-- YAML
added: v0.5.0
-->

The `os.arch()` method returns a string identifying the operating system CPU
architecture *for which the Node.js binary was compiled*.

The current possible values are: `'arm'`, `'arm64'`, `'ia32'`, `'mips'`,
`'mipsel'`, `'ppc'`, `'ppc64'`, `'s390'`, `'s390x'`, `'x32'`, `'x64'`,  and
`'x86'`.

Equivalent to [`process.arch`][].

