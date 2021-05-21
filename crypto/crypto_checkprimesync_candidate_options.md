<!-- YAML
added: v15.8.0
-->

* `candidate` {ArrayBuffer|SharedArrayBuffer|TypedArray|Buffer|DataView|bigint}
  A possible prime encoded as a sequence of big endian octets of arbitrary
  length.
* `options` {Object}
  * `checks` {number} The number of Miller-Rabin probabilistic primality
    iterations to perform. When the value is `0` (zero), a number of checks
    is used that yields a false positive rate of at most 2<sup>-64</sup> for
    random input. Care must be used when selecting a number of checks. Refer
    to the OpenSSL documentation for the [`BN_is_prime_ex`][] function `nchecks`
    options for more details. **Default:** `0`
* Returns: {boolean} `true` if the candidate is a prime with an error
  probability less than `0.25 ** options.checks`.

Checks the primality of the `candidate`.

