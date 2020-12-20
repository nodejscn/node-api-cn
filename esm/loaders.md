
> Stability: 1 - Experimental

**Note: This API is currently being redesigned and will still change.**

<!-- type=misc -->

To customize the default module resolution, loader hooks can optionally be
provided via a `--experimental-loader ./loader-name.mjs` argument to Node.js.

When hooks are used they only apply to ES module loading and not to any
CommonJS modules loaded.

