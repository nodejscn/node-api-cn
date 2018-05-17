<!-- YAML
added: v9.9.0
-->

* `env` {Object} An object containing the environment variables to check.
  **Default:** `process.env`.
* Returns: {number}

Returns:
* `1` for 2,
* `4` for 16,
* `8` for 256,
* `24` for 16,777,216
colors supported.

Use this to determine what colors the terminal supports. Due to the nature of
colors in terminals it is possible to either have false positives or false
negatives. It depends on process information and the environment variables that
may lie about what terminal is used.
To enforce a specific behavior without relying on `process.env` it is possible
to pass in an object with different settings.

Use the `NODE_DISABLE_COLORS` environment variable to enforce this function to
always return 1.

