<!-- YAML
added:
  - v14.8.0
  - v12.19.0
napiVersion: 8
-->

A 128-bit value stored as two unsigned 64-bit integers. It serves as a UUID
with which JavaScript objects can be "tagged" in order to ensure that they are
of a certain type. This is a stronger check than [`napi_instanceof`][], because
the latter can report a false positive if the object's prototype has been
manipulated. Type-tagging is most useful in conjunction with [`napi_wrap`][]
because it ensures that the pointer retrieved from a wrapped object can be
safely cast to the native type corresponding to the type tag that had been
previously applied to the JavaScript object.

```c
typedef struct {
  uint64_t lower;
  uint64_t upper;
} napi_type_tag;
```

