<!-- YAML
added: v6.6.0
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35093
    description: The a and b arguments can also be ArrayBuffer.
-->

* `a` {ArrayBuffer|Buffer|TypedArray|DataView}
* `b` {ArrayBuffer|Buffer|TypedArray|DataView}
* Returns: {boolean}

This function is based on a constant-time algorithm.
Returns true if `a` is equal to `b`, without leaking timing information that
would allow an attacker to guess one of the values. This is suitable for
comparing HMAC digests or secret values like authentication cookies or
[capability urls](https://www.w3.org/TR/capability-urls/).

`a` and `b` must both be `Buffer`s, `TypedArray`s, or `DataView`s, and they
must have the same byte length.

If at least one of `a` and `b` is a `TypedArray` with more than one byte per
entry, such as `Uint16Array`, the result will be computed using the platform
byte order.

Use of `crypto.timingSafeEqual` does not guarantee that the *surrounding* code
is timing-safe. Care should be taken to ensure that the surrounding code does
not introduce timing vulnerabilities.

