node --require "./a.js" --require "./b.js"
```

Node.js options that are allowed are:
<!-- node-options-node start -->
- `--enable-fips`
- `--es-module-specifier-resolution`
- `--experimental-exports`
- `--experimental-modules`
- `--experimental-policy`
- `--experimental-repl-await`
- `--experimental-report`
- `--experimental-vm-modules`
- `--experimental-wasm-modules`
- `--force-fips`
- `--frozen-intrinsics`
- `--heapsnapshot-signal`
- `--http-parser`
- `--http-server-default-timeout`
- `--icu-data-dir`
- `--input-type`
- `--inspect-brk`
- `--inspect-port`, `--debug-port`
- `--inspect-publish-uid`
- `--inspect`
- `--loader`
- `--max-http-header-size`
- `--napi-modules`
- `--no-deprecation`
- `--no-force-async-hooks-checks`
- `--no-warnings`
- `--openssl-config`
- `--pending-deprecation`
- `--policy-integrity`
- `--preserve-symlinks-main`
- `--preserve-symlinks`
- `--prof-process`
- `--redirect-warnings`
- `--report-directory`
- `--report-filename`
- `--report-on-fatalerror`
- `--report-on-signal`
- `--report-signal`
- `--report-uncaught-exception`
- `--require`, `-r`
- `--throw-deprecation`
- `--title`
- `--tls-cipher-list`
- `--tls-max-v1.2`
- `--tls-max-v1.3`
- `--tls-min-v1.0`
- `--tls-min-v1.1`
- `--tls-min-v1.2`
- `--tls-min-v1.3`
- `--trace-deprecation`
- `--trace-event-categories`
- `--trace-event-file-pattern`
- `--trace-events-enabled`
- `--trace-sync-io`
- `--trace-tls`
- `--trace-warnings`
- `--track-heap-objects`
- `--unhandled-rejections`
- `--use-bundled-ca`
- `--use-openssl-ca`
- `--v8-pool-size`
- `--zero-fill-buffers`
<!-- node-options-node end -->

V8 options that are allowed are:
<!-- node-options-v8 start -->
- `--abort-on-uncaught-exception`
- `--max-old-space-size`
- `--perf-basic-prof-only-functions`
- `--perf-basic-prof`
- `--perf-prof-unwinding-info`
- `--perf-prof`
- `--stack-trace-limit`
<!-- node-options-v8 end -->

