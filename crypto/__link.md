[`Buffer`]: buffer.html
[`EVP_BytesToKey`]: https://www.openssl.org/docs/man1.0.2/crypto/EVP_BytesToKey.html
[`UV_THREADPOOL_SIZE`]: cli.html#cli_uv_threadpool_size_size
[`cipher.final()`]: #crypto_cipher_final_outputencoding
[`cipher.update()`]: #crypto_cipher_update_data_inputencoding_outputencoding
[`crypto.createCipher()`]: #crypto_crypto_createcipher_algorithm_password_options
[`crypto.createCipheriv()`]: #crypto_crypto_createcipheriv_algorithm_key_iv_options
[`crypto.createDecipher()`]: #crypto_crypto_createdecipher_algorithm_password_options
[`crypto.createDecipheriv()`]: #crypto_crypto_createdecipheriv_algorithm_key_iv_options
[`crypto.createDiffieHellman()`]: #crypto_crypto_creatediffiehellman_prime_primeencoding_generator_generatorencoding
[`crypto.createECDH()`]: #crypto_crypto_createecdh_curvename
[`crypto.createHash()`]: #crypto_crypto_createhash_algorithm_options
[`crypto.createHmac()`]: #crypto_crypto_createhmac_algorithm_key_options
[`crypto.createSign()`]: #crypto_crypto_createsign_algorithm_options
[`crypto.createVerify()`]: #crypto_crypto_createverify_algorithm_options
[`crypto.getCurves()`]: #crypto_crypto_getcurves
[`crypto.getHashes()`]: #crypto_crypto_gethashes
[`crypto.pbkdf2()`]: #crypto_crypto_pbkdf2_password_salt_iterations_keylen_digest_callback
[`crypto.randomBytes()`]: #crypto_crypto_randombytes_size_callback
[`crypto.randomFill()`]: #crypto_crypto_randomfill_buffer_offset_size_callback
[`decipher.final()`]: #crypto_decipher_final_outputencoding
[`decipher.update()`]: #crypto_decipher_update_data_inputencoding_outputencoding
[`diffieHellman.setPublicKey()`]: #crypto_diffiehellman_setpublickey_publickey_encoding
[`ecdh.generateKeys()`]: #crypto_ecdh_generatekeys_encoding_format
[`ecdh.setPrivateKey()`]: #crypto_ecdh_setprivatekey_privatekey_encoding
[`ecdh.setPublicKey()`]: #crypto_ecdh_setpublickey_publickey_encoding
[`hash.digest()`]: #crypto_hash_digest_encoding
[`hash.update()`]: #crypto_hash_update_data_inputencoding
[`hmac.digest()`]: #crypto_hmac_digest_encoding
[`hmac.update()`]: #crypto_hmac_update_data_inputencoding
[`sign.sign()`]: #crypto_sign_sign_privatekey_outputformat
[`sign.update()`]: #crypto_sign_update_data_inputencoding
[`stream.transform` options]: stream.html#stream_new_stream_transform_options
[`stream.Writable` options]: stream.html#stream_constructor_new_stream_writable_options
[`tls.createSecureContext()`]: tls.html#tls_tls_createsecurecontext_options
[`verify.update()`]: #crypto_verify_update_data_inputencoding
[`verify.verify()`]: #crypto_verify_verify_object_signature_signatureformat
[Caveats]: #crypto_support_for_weak_or_compromised_algorithms
[Crypto Constants]: #crypto_crypto_constants_1
[HTML5's `keygen` element]: http://www.w3.org/TR/html5/forms.html#the-keygen-element
[NIST SP 800-131A]: http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar1.pdf
[NIST SP 800-132]: http://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-132.pdf
[Nonce-Disrespecting Adversaries]: https://github.com/nonce-disrespect/nonce-disrespect
[OpenSSL's SPKAC implementation]: https://www.openssl.org/docs/man1.0.2/apps/spkac.html
[RFC 2412]: https://www.rfc-editor.org/rfc/rfc2412.txt
[RFC 3526]: https://www.rfc-editor.org/rfc/rfc3526.txt
[RFC 4055]: https://www.rfc-editor.org/rfc/rfc4055.txt
[initialization vector]: https://en.wikipedia.org/wiki/Initialization_vector
[stream-writable-write]: stream.html#stream_writable_write_chunk_encoding_callback
[stream]: stream.html