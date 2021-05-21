<!-- YAML
added: v15.6.0
-->

Initializes an OpenSSL secure heap of `n` bytes. When initialized, the
secure heap is used for selected types of allocations within OpenSSL
during key generation and other operations. This is useful, for instance,
to prevent sensitive information from leaking due to pointer overruns
or underruns.

The secure heap is a fixed size and cannot be resized at runtime so,
if used, it is important to select a large enough heap to cover all
application uses.

The heap size given must be a power of two. Any value less than 2
will disable the secure heap.

The secure heap is disabled by default.

The secure heap is not available on Windows.

See [`CRYPTO_secure_malloc_init`][] for more details.

