<!-- YAML
added: v0.1.101
-->

Uses [`util.inspect()`][] on `obj` and prints the resulting string to `stdout`.
This function bypasses any custom `inspect()` function defined on `obj`. An
optional `options` object may be passed to alter certain aspects of the
formatted string:

- `showHidden` - if `true` then the object's non-enumerable and symbol
properties will be shown too. Defaults to `false`.

- `depth` - tells [`util.inspect()`][] how many times to recurse while
formatting the object. This is useful for inspecting large complicated objects.
Defaults to `2`. To make it recurse indefinitely, pass `null`.

- `colors` - if `true`, then the output will be styled with ANSI color codes.
Defaults to `false`. Colors are customizable; see
[customizing `util.inspect()` colors][].

