
[`process.setUncaughtExceptionCaptureCallback()`][] was called twice,
without first resetting the callback to `null`.

This error is designed to prevent accidentally overwriting a callback registered
from another module.

<a id="ERR_UNESCAPED_CHARACTERS"></a>
