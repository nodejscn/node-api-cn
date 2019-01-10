
Instantiate the module. This must be called after linking has completed
(`linkingStatus` is `'linked'`); otherwise it will throw an error. It may also
throw an exception if one of the dependencies does not provide an export the
parent module requires.

However, if this function succeeded, further calls to this function after the
initial instantiation will be no-ops, to be consistent with the ECMAScript
specification.

Unlike other methods operating on `Module`, this function completes
synchronously and returns nothing.

Corresponds to the [Instantiate() concrete method][] field of [Source Text
Module Record][]s in the ECMAScript specification.

