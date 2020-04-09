
Additional runtime configuration of report generation is available via
the following properties of `process.report`:

`reportOnFatalError` triggers diagnostic reporting on fatal errors when `true`.
Defaults to `false`.

`reportOnSignal` triggers diagnostic reporting on signal when `true`. This is
not supported on Windows. Defaults to `false`.

`reportOnUncaughtException` triggers diagnostic reporting on uncaught exception
when `true`. Defaults to `false`.

`signal` specifies the POSIX signal identifier that will be used
to intercept external triggers for report generation. Defaults to
`'SIGUSR2'`.

`filename` specifies the name of the output file in the file system.
Special meaning is attached to `stdout` and `stderr`. Usage of these
will result in report being written to the associated standard streams.
In cases where standard streams are used, the value in `directory` is ignored.
URLs are not supported. Defaults to a composite filename that contains
timestamp, PID and sequence number.

`directory` specifies the filesystem directory where the report will be written.
URLs are not supported. Defaults to the current working directory of the
Node.js process.

```js
// Trigger report only on uncaught exceptions.
process.report.reportOnFatalError = false;
process.report.reportOnSignal = false;
process.report.reportOnUncaughtException = true;

// Trigger report for both internal errors as well as external signal.
process.report.reportOnFatalError = true;
process.report.reportOnSignal = true;
process.report.reportOnUncaughtException = false;

// Change the default signal to 'SIGQUIT' and enable it.
process.report.reportOnFatalError = false;
process.report.reportOnUncaughtException = false;
process.report.reportOnSignal = true;
process.report.signal = 'SIGQUIT';
```

Configuration on module initialization is also available via
environment variables:

```bash
NODE_OPTIONS="--experimental-report --report-uncaught-exception \
  --report-on-fatalerror --report-on-signal \
  --report-signal=SIGUSR2  --report-filename=./report.json \
  --report-directory=/home/nodeuser"
```

Specific API documentation can be found under
[`process API documentation`][] section.

