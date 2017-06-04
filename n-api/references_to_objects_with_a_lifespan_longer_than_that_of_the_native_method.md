In some cases an addon will need to be able to create and reference objects
with a lifespan longer than that of a single native method invocation. For
example, to create a constructor and later use that constructor
in a request to creates instances, it must be possible to reference
the constructor object across many different instance creation requests. This
would not be possible with a normal handle returned as a `napi_value` as
described in the earlier section. The lifespan of a normal handle is
managed by scopes and all scopes must be closed before the end of a native
method.

N-API provides methods to create persistent references to an object.
Each persistent reference has an associated count with a value of 0
or higher. The count determines if the reference will keep
the corresponding object live. References with a count of 0 do not
prevent the object from being collected and are often called 'weak'
references. Any count greater than 0 will prevent the object
from being collected.

References can be created with an initial reference count. The count can
then be modified through [`napi_reference_ref`][] and
[`napi_reference_unref`][]. If an object is collected while the count
for a reference is 0, all subsequent calls to
get the object associated with the reference [`napi_get_reference_value`][]
will return NULL for the returned `napi_value`. An attempt to call
[`napi_reference_ref`][] for a reference whose object has been collected
will result in an error.

References must be deleted once they are no longer required by the addon. When
a reference is deleted it will no longer prevent the corresponding object from
being collected. Failure to delete a persistent reference will result in
a 'memory leak' with both the native memory for the persistent reference and
the corresponding object on the heap being retained forever.

There can be multiple persistent references created which refer to the same
object, each of which will either keep the object live or not based on its
individual count.

