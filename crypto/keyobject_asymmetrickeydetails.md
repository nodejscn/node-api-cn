<!-- YAML
added: v15.7.0
-->

* {Object}
  * `modulusLength`: {number} Key size in bits (RSA, DSA).
  * `publicExponent`: {bigint} Public exponent (RSA).
  * `divisorLength`: {number} Size of `q` in bits (DSA).
  * `namedCurve`: {string} Name of the curve (EC).

This property exists only on asymmetric keys. Depending on the type of the key,
this object contains information about the key. None of the information obtained
through this property can be used to uniquely identify a key or to compromise
the security of the key.

RSA-PSS parameters, DH, or any future key type details might be exposed via this
API using additional attributes.

