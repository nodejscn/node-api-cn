
The `domain` module was not usable since it could not establish the required
error handling hooks, because
[`process.setUncaughtExceptionCaptureCallback()`][] had been called at an
earlier point in time.

<a id="ERR_DOMAIN_CANNOT_SET_UNCAUGHT_EXCEPTION_CAPTURE"></a>
