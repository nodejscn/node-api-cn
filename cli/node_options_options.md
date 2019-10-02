<!-- YAML
added: v8.0.0
-->

A space-separated list of command line options. `options...` are interpreted
before command line options, so command line options will override or
compound after anything in `options...`. Node.js will exit with an error if
an option that is not allowed in the environment is used, such as `-p` or a
script file.

In case an option value happens to contain a space (for example a path listed
in `--require`), it must be escaped using double quotes. For example:

```bash
NODE_OPTIONS='--require "./my path/file.js"'
```

A singleton flag passed as a command line option will override the same flag
passed into `NODE_OPTIONS`:

```bash
# The inspector will be available on port 5555
NODE_OPTIONS='--inspect=localhost:4444' node --inspect=localhost:5555
```

A flag that can be passed multiple times will be treated as if its
`NODE_OPTIONS` instances were passed first, and then its command line
instances afterwards:

```bash
NODE_OPTIONS='--require "./a.js"' node --require "./b.js"
# is equivalent to:
node --require "./a.js" --require "./b.js"
```

Node.js options that are allowed are:
<!-- node-options-node start -->
* `--enable-fips`
* `--es-module-specifier-resolution`
* `--experimental-exports`
* `--experimental-loader`
* `--experimental-modules`
* `--experimental-policy`
* `--experimental-repl-await`
* `--experimental-report`
* `--experimental-vm-modules`
* `--experimental-wasm-modules`
* `--force-fips`
* `--frozen-intrinsics`
* `--heapsnapshot-signal`
* `--http-parser`
* `--http-server-default-timeout`
* `--icu-data-dir`
* `--input-type`
* `--inspect-brk`
* `--inspect-port`, `--debug-port`
* `--inspect-publish-uid`
* `--inspect`
* `--max-http-header-size`
* `--napi-modules`
* `--no-deprecation`
* `--no-force-async-hooks-checks`
* `--no-warnings`
* `--openssl-config`
* `--pending-deprecation`
* `--policy-integrity`
* `--preserve-symlinks-main`
* `--preserve-symlinks`
* `--prof-process`
* `--redirect-warnings`
* `--report-directory`
* `--report-filename`
* `--report-on-fatalerror`
* `--report-on-signal`
* `--report-signal`
* `--report-uncaught-exception`
* `--require`, `-r`
* `--throw-deprecation`
* `--title`
* `--tls-cipher-list`
* `--tls-max-v1.2`
* `--tls-max-v1.3`
* `--tls-min-v1.0`
* `--tls-min-v1.1`
* `--tls-min-v1.2`
* `--tls-min-v1.3`
* `--trace-deprecation`
* `--trace-event-categories`
* `--trace-event-file-pattern`
* `--trace-events-enabled`
* `--trace-sync-io`
* `--trace-tls`
* `--trace-warnings`
* `--track-heap-objects`
* `--unhandled-rejections`
* `--use-bundled-ca`
* `--use-openssl-ca`
* `--v8-pool-size`
* `--zero-fill-buffers`
<!-- node-options-node end -->

V8 options that are allowed are:
<!-- node-options-v8 start -->
* `--abort-on-uncaught-exception`
* `--interpreted-frames-native-stack`
* `--max-old-space-size`
* `--perf-basic-prof-only-functions`
* `--perf-basic-prof`
* `--perf-prof-unwinding-info`
* `--perf-prof`
* `--stack-trace-limit`
<!-- node-options-v8 end -->

