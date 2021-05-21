
While a Node.js process typically releases all its resources when exiting,
embedders of Node.js, or future Worker support, may require addons to register
clean-up hooks that will be run once the current Node.js instance exits.

Node-API provides functions for registering and un-registering such callbacks.
When those callbacks are run, all resources that are being held by the addon
should be freed up.

