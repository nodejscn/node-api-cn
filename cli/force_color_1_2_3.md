
The `FORCE_COLOR` environment variable is used to
enable ANSI colorized output. The value may be:

* `1`, `true`, or the empty string `''` indicate 16-color support,
* `2` to indicate 256-color support, or
* `3` to indicate 16 million-color support.

When `FORCE_COLOR` is used and set to a supported value, both the `NO_COLOR`,
and `NODE_DISABLE_COLORS` environment variables are ignored.

Any other value will result in colorized output being disabled.
