<!-- YAML
added:
 - v13.3.0
 - v12.16.0
-->

The `WASI` class provides the WASI system call API and additional convenience
methods for working with WASI-based applications. Each `WASI` instance
represents a distinct sandbox environment. For security purposes, each `WASI`
instance must have its command line arguments, environment variables, and
sandbox directory structure configured explicitly.

