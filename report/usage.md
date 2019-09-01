
```bash
node --experimental-report --report-uncaught-exception \
  --report-on-signal --report-on-fatalerror app.js
```

* `--experimental-report` Enables the diagnostic report feature.
 In the absence of this flag, use of all other related options will result in
 an error.

* `--report-uncaught-exception` Enables report to be generated on
un-caught exceptions. Useful when inspecting JavaScript stack in conjunction
with native stack and other runtime environment data.

* `--report-on-signal` Enables report to be generated upon receiving
the specified (or predefined) signal to the running Node.js process. (See below
on how to modify the signal that triggers the report.) Default signal is `SIGUSR2`.
Useful when a report needs to be triggered from another program.
Application monitors may leverage this feature to collect report at regular
intervals and plot rich set of internal runtime data to their views.

Signal based report generation is not supported in Windows.

Under normal circumstances, there is no need to modify the report triggering
signal. However, if `SIGUSR2` is already used for other purposes, then this
flag helps to change the signal for report generation and preserve the original
meaning of `SIGUSR2` for the said purposes.

* `--report-on-fatalerror` Enables the report to be triggered on
fatal errors (internal errors within the Node.js runtime, such as out of memory)
that leads to termination of the application. Useful to inspect various
diagnostic data elements such as heap, stack, event loop state, resource
consumption etc. to reason about the fatal error.

* `--report-directory` Location at which the report will be
generated.

* `--report-filename` Name of the file to which the report will be
written.

* `--report-signal` Sets or resets the signal for report generation
(not supported on Windows). Default signal is `SIGUSR2`.

A report can also be triggered via an API call from a JavaScript application:

```js
process.report.writeReport();
```

This function takes an optional additional argument `filename`, which is
the name of a file into which the report is written.

```js
process.report.writeReport('./foo.json');
```

This function takes an optional additional argument `err` - an `Error` object
that will be used as the context for the JavaScript stack printed in the report.
When using report to handle errors in a callback or an exception handler, this
allows the report to include the location of the original error as well
as where it was handled.

```js
try {
  process.chdir('/non-existent-path');
} catch (err) {
  process.report.writeReport(err);
}
// Any other code
```

If both filename and error object are passed to `writeReport()` the
error object must be the second parameter.

```js
try {
  process.chdir('/non-existent-path');
} catch (err) {
  process.report.writeReport(filename, err);
}
// Any other code
```

The content of the diagnostic report can be returned as a JavaScript Object
via an API call from a JavaScript application:

```js
const report = process.report.getReport();
console.log(typeof report === 'object'); // true

// Similar to process.report.writeReport() output
console.log(JSON.stringify(report, null, 2));
```

This function takes an optional additional argument `err` - an `Error` object
that will be used as the context for the JavaScript stack printed in the report.

```js
const report = process.report.getReport(new Error('custom error'));
console.log(typeof report === 'object'); // true
```

The API versions are useful when inspecting the runtime state from within
the application, in expectation of self-adjusting the resource consumption,
load balancing, monitoring etc.

The content of the report consists of a header section containing the event
type, date, time, PID and Node.js version, sections containing JavaScript and
native stack traces, a section containing V8 heap information, a section
containing `libuv` handle information and an OS platform information section
showing CPU and memory usage and system limits. An example report can be
triggered using the Node.js REPL:

```raw
$ node
> process.report.writeReport();
Writing Node.js report to file: report.20181126.091102.8480.0.001.json
Node.js report completed
>
```

When a report is written, start and end messages are issued to stderr
and the filename of the report is returned to the caller. The default filename
includes the date, time, PID and a sequence number. The sequence number helps
in associating the report dump with the runtime state if generated multiple
times for the same Node.js process.

