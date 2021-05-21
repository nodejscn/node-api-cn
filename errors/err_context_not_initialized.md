
The vm context passed into the API is not yet initialized. This could happen
when an error occurs (and is caught) during the creation of the
context, for example, when the allocation fails or the maximum call stack
size is reached when the context is created.

<a id="ERR_CRYPTO_CUSTOM_ENGINE_NOT_SUPPORTED"></a>
