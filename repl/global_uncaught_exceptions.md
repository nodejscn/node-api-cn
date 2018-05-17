
The REPL uses the [`domain`][] module to catch all uncaught exceptions for that
REPL session.

This use of the [`domain`][] module in the REPL has these side effects:

* Uncaught exceptions do not emit the [`'uncaughtException'`][] event.
* Trying to use [`process.setUncaughtExceptionCaptureCallback()`][] throws
  an [`ERR_DOMAIN_CANNOT_SET_UNCAUGHT_EXCEPTION_CAPTURE`][] error.

