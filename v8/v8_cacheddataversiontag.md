<!-- YAML
added: v8.0.0
-->

Returns an integer representing a "version tag" derived from the V8 version,
command line flags and detected CPU features. This is useful for determining
whether a [`vm.Script`][] `cachedData` buffer is compatible with this instance
of V8.

