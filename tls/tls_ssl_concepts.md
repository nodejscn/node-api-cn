
The TLS/SSL is a public/private key infrastructure (PKI). For most common
cases, each client and server must have a *private key*.

Private keys can be generated in multiple ways. The example below illustrates
use of the OpenSSL command-line interface to generate a 2048-bit RSA private
key:

```sh
openssl genrsa -out ryans-key.pem 2048
```

With TLS/SSL, all servers (and some clients) must have a *certificate*.
Certificates are *public keys* that correspond to a private key, and that are
digitally signed either by a Certificate Authority or by the owner of the
private key (such certificates are referred to as "self-signed"). The first
step to obtaining a certificate is to create a *Certificate Signing Request*
(CSR) file.

The OpenSSL command-line interface can be used to generate a CSR for a private
key:

```sh
openssl req -new -sha256 -key ryans-key.pem -out ryans-csr.pem
```

Once the CSR file is generated, it can either be sent to a Certificate
Authority for signing or used to generate a self-signed certificate.

Creating a self-signed certificate using the OpenSSL command-line interface
is illustrated in the example below:

```sh
openssl x509 -req -in ryans-csr.pem -signkey ryans-key.pem -out ryans-cert.pem
```

Once the certificate is generated, it can be used to generate a `.pfx` or
`.p12` file:

```sh
openssl pkcs12 -export -in ryans-cert.pem -inkey ryans-key.pem \
      -certfile ca-cert.pem -out ryans.pfx
```

Where:

* `in`: is the signed certificate
* `inkey`: is the associated private key
* `certfile`: is a concatenation of all Certificate Authority (CA) certs into
   a single file, e.g. `cat ca1-cert.pem ca2-cert.pem > ca-cert.pem`

