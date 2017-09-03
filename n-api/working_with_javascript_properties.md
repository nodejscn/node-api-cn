
N-API exposes a set of APIs to get and set properties on JavaScript
objects. Some of these types are documented under
[Section 7](https://tc39.github.io/ecma262/#sec-operations-on-objects) of the
[ECMAScript Language Specification](https://tc39.github.io/ecma262/).

Properties in JavaScript are represented as a tuple of a key and a value.
Fundamentally, all property keys in N-API can be represented in one of the
following forms:
- Named: a simple UTF8-encoded string
- Integer-Indexed: an index value represented by `uint32_t`
- JavaScript value: these are represented in N-API by `napi_value`. This can
be a `napi_value` representing a String, Number or Symbol.

N-API values are represented by the type `napi_value`.
Any N-API call that requires a JavaScript value takes in a `napi_value`.
However, it's the caller's responsibility to make sure that the
`napi_value` in question is of the JavaScript type expected by the API.

The APIs documented in this section provide a simple interface to
get and set properties on arbitrary JavaScript objects represented by
`napi_value`.

For instance, consider the following JavaScript code snippet:
```js
const obj = {};
obj.myProp = 123;
```
The equivalent can be done using N-API values with the following snippet:
```C
napi_status status = napi_generic_failure;

// const obj = {}
napi_value obj, value;
status = napi_create_object(env, &obj);
if (status != napi_ok) return status;

// Create a napi_value for 123
status = napi_create_int32(env, 123, &value);
if (status != napi_ok) return status;

// obj.myProp = 123
status = napi_set_named_property(env, obj, "myProp", value);
if (status != napi_ok) return status;
```

Indexed properties can be set in a similar manner. Consider the following
JavaScript snippet:
```js
const arr = [];
arr[123] = 'hello';
```
The equivalent can be done using N-API values with the following snippet:
```C
napi_status status = napi_generic_failure;

// const arr = [];
napi_value arr, value;
status = napi_create_array(env, &arr);
if (status != napi_ok) return status;

// Create a napi_value for 'hello'
status = napi_create_string_utf8(env, "hello", -1, &value);
if (status != napi_ok) return status;

// arr[123] = 'hello';
status = napi_set_element(env, arr, 123, value);
if (status != napi_ok) return status;
```

Properties can be retrieved using the APIs described in this section.
Consider the following JavaScript snippet:
```js
const arr = [];
const value = arr[123];
```

The following is the approximate equivalent of the N-API counterpart:
```C
napi_status status = napi_generic_failure;

// const arr = []
napi_value arr, value;
status = napi_create_array(env, &arr);
if (status != napi_ok) return status;

// const value = arr[123]
status = napi_get_element(env, arr, 123, &value);
if (status != napi_ok) return status;
```

Finally, multiple properties can also be defined on an object for performance
reasons. Consider the following JavaScript:
```js
const obj = {};
Object.defineProperties(obj, {
  'foo': { value: 123, writable: true, configurable: true, enumerable: true },
  'bar': { value: 456, writable: true, configurable: true, enumerable: true }
});
```

The following is the approximate equivalent of the N-API counterpart:
```C
napi_status status = napi_status_generic_failure;

// const obj = {};
napi_value obj;
status = napi_create_obj(env, &obj);
if (status != napi_ok) return status;

// Create napi_values for 123 and 456
napi_value fooValue, barValue;
status = napi_create_int32(env, 123, &fooValue);
if (status != napi_ok) return status;
status = napi_create_int32(env, 456, &barValue);
if (status != napi_ok) return status;

// Set the properties
napi_property_descriptors descriptors[] = {
  { "foo", fooValue, 0, 0, 0, napi_default, 0 },
  { "bar", barValue, 0, 0, 0, napi_default, 0 }
}
status = napi_define_properties(env,
                                obj,
                                sizeof(descriptors) / sizeof(descriptors[0]),
                                descriptors);
if (status != napi_ok) return status;
```

