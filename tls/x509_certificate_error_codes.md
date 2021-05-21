
Multiple functions can fail due to certificate errors that are reported by
OpenSSL. In such a case, the function provides an {Error} via its callback that
has the property `code` which can take one of the following values:

<!--
values are taken from src/crypto/crypto_common.cc
description are taken from deps/openssl/openssl/crypto/x509/x509_txt.c
-->
* `'UNABLE_TO_GET_ISSUER_CERT'`: Unable to get issuer certificate.
* `'UNABLE_TO_GET_CRL'`: Unable to get certificate CRL.
* `'UNABLE_TO_DECRYPT_CERT_SIGNATURE'`: Unable to decrypt certificate's
  signature.
* `'UNABLE_TO_DECRYPT_CRL_SIGNATURE'`: Unable to decrypt CRL's signature.
* `'UNABLE_TO_DECODE_ISSUER_PUBLIC_KEY'`: Unable to decode issuer public key.
* `'CERT_SIGNATURE_FAILURE'`: Certificate signature failure.
* `'CRL_SIGNATURE_FAILURE'`: CRL signature failure.
* `'CERT_NOT_YET_VALID'`: Certificate is not yet valid.
* `'CERT_HAS_EXPIRED'`: Certificate has expired.
* `'CRL_NOT_YET_VALID'`: CRL is not yet valid.
* `'CRL_HAS_EXPIRED'`: CRL has expired.
* `'ERROR_IN_CERT_NOT_BEFORE_FIELD'`: Format error in certificate's notBefore
  field.
* `'ERROR_IN_CERT_NOT_AFTER_FIELD'`: Format error in certificate's notAfter
  field.
* `'ERROR_IN_CRL_LAST_UPDATE_FIELD'`: Format error in CRL's lastUpdate field.
* `'ERROR_IN_CRL_NEXT_UPDATE_FIELD'`: Format error in CRL's nextUpdate field.
* `'OUT_OF_MEM'`: Out of memory.
* `'DEPTH_ZERO_SELF_SIGNED_CERT'`: Self signed certificate.
* `'SELF_SIGNED_CERT_IN_CHAIN'`: Self signed certificate in certificate chain.
* `'UNABLE_TO_GET_ISSUER_CERT_LOCALLY'`: Unable to get local issuer certificate.
* `'UNABLE_TO_VERIFY_LEAF_SIGNATURE'`: Unable to verify the first certificate.
* `'CERT_CHAIN_TOO_LONG'`: Certificate chain too long.
* `'CERT_REVOKED'`: Certificate revoked.
* `'INVALID_CA'`: Invalid CA certificate.
* `'PATH_LENGTH_EXCEEDED'`: Path length constraint exceeded.
* `'INVALID_PURPOSE'`: Unsupported certificate purpose.
* `'CERT_UNTRUSTED'`: Certificate not trusted.
* `'CERT_REJECTED'`: Certificate rejected.
* `'HOSTNAME_MISMATCH'`: Hostname mismatch.

