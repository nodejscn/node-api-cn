<!-- YAML
added: v0.1.16
deprecated: v14.6.0
-->

> Stability: 0 - Deprecated: Please use [`require.main`][] and
> [`module.children`][] instead.

* {module | null | undefined}

The module that first required this one, or `null` if the current module is the
entry point of the current process, or `undefined` if the module was loaded by
something that is not a CommonJS module (E.G.: REPL or `import`).

