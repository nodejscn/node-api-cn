<!-- YAML
added: v11.12.0
-->

> Stability: 1 - Experimental

Enable experimental frozen intrinsics like `Array` and `Object`.

Support is currently only provided for the root context and no guarantees are
currently provided that `global.Array` is indeed the default intrinsic
reference. Code may break under this flag.

`--require` runs prior to freezing intrinsics in order to allow polyfills to
be added.

