
<!-- type=misc -->

To customize the default module resolution, loader hooks can optionally be
provided via a `--loader ./loader-name.mjs` argument to Node.

When hooks are used they only apply to ES module loading and not to any
CommonJS modules loaded.

