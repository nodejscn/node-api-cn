
The `crypto` module still supports some algorithms which are already
compromised and are not currently recommended for use. The API also allows
the use of ciphers and hashes with a small key size that are considered to be
too weak for safe use.

Users should take full responsibility for selecting the crypto
algorithm and key size according to their security requirements.

Based on the recommendations of [NIST SP 800-131A][]:

- MD5 and SHA-1 are no longer acceptable where collision resistance is
  required such as digital signatures.
- The key used with RSA, DSA and DH algorithms is recommended to have
  at least 2048 bits and that of the curve of ECDSA and ECDH at least
  224 bits, to be safe to use for several years.
- The DH groups of `modp1`, `modp2` and `modp5` have a key size
  smaller than 2048 bits and are not recommended.

See the reference for other recommendations and details.

