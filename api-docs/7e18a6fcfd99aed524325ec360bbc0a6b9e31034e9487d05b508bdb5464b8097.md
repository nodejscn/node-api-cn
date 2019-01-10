<!-- YAML
added: v10.2.0
-->

Instructs the module loader to preserve symbolic links when resolving and
caching the main module (`require.main`).

This flag exists so that the main module can be opted-in to the same behavior
that `--preserve-symlinks` gives to all other imports; they are separate flags,
however, for backward compatibility with older Node.js versions.

Note that `--preserve-symlinks-main` does not imply `--preserve-symlinks`; it
is expected that `--preserve-symlinks-main` will be used in addition to
`--preserve-symlinks` when it is not desirable to follow symlinks before
resolving relative paths.

See `--preserve-symlinks` for more information.

