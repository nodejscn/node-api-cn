The simple asynchronous work APIs above may not be appropriate for every
scenario, because with those the async execution still happens on the main
event loop. When using any other async mechanism, the following APIs are
necessary to ensure an async operation is properly tracked by the runtime.

