<!-- YAML
added: v8.0.0
-->

When set to `1`, emit pending deprecation warnings.

*Note*: Pending deprecations are generally identical to a runtime deprecation
with the notable exception that they are turned *off* by default and will not
be emitted unless either the `--pending-deprecation` command line flag, or the
`NODE_PENDING_DEPRECATION=1` environment variable, is set. Pending deprecations
are used to provide a kind of selective "early warning" mechanism that
developers may leverage to detect deprecated API usage.

