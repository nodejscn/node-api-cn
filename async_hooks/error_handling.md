
If any `AsyncHook` callbacks throw, the application will print the stack trace
and exit. The exit path does follow that of an uncaught exception but
all `uncaughtException` listeners are removed, thus forcing the process to
exit. The `'exit'` callbacks will still be called unless the application is run
with `--abort-on-uncaught-exception`, in which case a stack trace will be
printed and the application exits, leaving a core file.

The reason for this error handling behavior is that these callbacks are running
at potentially volatile points in an object's lifetime, for example during
class construction and destruction. Because of this, it is deemed necessary to
bring down the process quickly in order to prevent an unintentional abort in the
future. This is subject to change in the future if a comprehensive analysis is
performed to ensure an exception can follow the normal control flow without
unintentional side effects.


