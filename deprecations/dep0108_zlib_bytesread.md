
Type: Documentation-only

Deprecated alias for [`zlib.bytesWritten`][]. This original name was chosen
because it also made sense to interpret the value as the number of bytes
read by the engine, but is inconsistent with other streams in Node.js that
expose values under these names.

[`--pending-deprecation`]: cli.html#cli_pending_deprecation
[`Buffer.allocUnsafeSlow(size)`]: buffer.html#buffer_class_method_buffer_allocunsafeslow_size
[`Buffer.from(array)`]: buffer.html#buffer_class_method_buffer_from_array
[`Buffer.from(buffer)`]: buffer.html#buffer_class_method_buffer_from_buffer
[`Buffer.isBuffer()`]: buffer.html#buffer_class_method_buffer_isbuffer_obj
[`Cipher`]: crypto.html#crypto_class_cipher
[`Decipher`]: crypto.html#crypto_class_decipher
[`assert`]: assert.html
[`clearInterval()`]: timers.html#timers_clearinterval_timeout
[`clearTimeout()`]: timers.html#timers_cleartimeout_timeout
[`EventEmitter.listenerCount(emitter, eventName)`]: events.html#events_eventemitter_listenercount_emitter_eventname
[`Server.connections`]: net.html#net_server_connections
[`Server.getConnections()`]: net.html#net_server_getconnections_callback
[`Server.listen({fd: <number>})`]: net.html#net_server_listen_handle_backlog_callback
[`SlowBuffer`]: buffer.html#buffer_class_slowbuffer
[`asyncResource.runInAsyncScope()`]: async_hooks.html#async_hooks_asyncresource_runinasyncscope_fn_thisarg_args
[`child_process`]: child_process.html
[`console.error()`]: console.html#console_console_error_data_args
[`console.log()`]: console.html#console_console_log_data_args
[`crypto.createCipher()`]: crypto.html#crypto_crypto_createcipher_algorithm_password_options
[`crypto.createCipheriv()`]: crypto.html#crypto_crypto_createcipheriv_algorithm_key_iv_options
[`crypto.createCredentials()`]: crypto.html#crypto_crypto_createcredentials_details
[`crypto.createDecipher()`]: crypto.html#crypto_crypto_createdecipher_algorithm_password_options
[`crypto.createDecipheriv()`]: crypto.html#crypto_crypto_createdecipheriv_algorithm_key_iv_options
[`crypto.DEFAULT_ENCODING`]: crypto.html#crypto_crypto_default_encoding
[`crypto.fips`]: crypto.html#crypto_crypto_fips
[`crypto.pbkdf2()`]: crypto.html#crypto_crypto_pbkdf2_password_salt_iterations_keylen_digest_callback
[`decipher.final()`]: crypto.html#crypto_decipher_final_outputencoding
[`decipher.setAuthTag()`]: crypto.html#crypto_decipher_setauthtag_buffer
[`domain`]: domain.html
[`ecdh.setPublicKey()`]: crypto.html#crypto_ecdh_setpublickey_publickey_encoding
[`emitter.listenerCount(eventName)`]: events.html#events_emitter_listenercount_eventname
[`fs.access()`]: fs.html#fs_fs_access_path_mode_callback
[`fs.exists(path, callback)`]: fs.html#fs_fs_exists_path_callback
[`fs.lchmod(path, mode, callback)`]: fs.html#fs_fs_lchmod_path_mode_callback
[`fs.lchmodSync(path, mode)`]: fs.html#fs_fs_lchmodsync_path_mode
[`fs.lchown(path, uid, gid, callback)`]: fs.html#fs_fs_lchown_path_uid_gid_callback
[`fs.lchownSync(path, uid, gid)`]: fs.html#fs_fs_lchownsync_path_uid_gid
[`fs.read()`]: fs.html#fs_fs_read_fd_buffer_offset_length_position_callback
[`fs.readSync()`]: fs.html#fs_fs_readsync_fd_buffer_offset_length_position
[`fs.stat()`]: fs.html#fs_fs_stat_path_callback
[`os.networkInterfaces`]: os.html#os_os_networkinterfaces
[`os.tmpdir()`]: os.html#os_os_tmpdir
[`process.env`]: process.html#process_process_env
[`punycode`]: punycode.html
[`require.extensions`]: modules.html#modules_require_extensions
[`setInterval()`]: timers.html#timers_setinterval_callback_delay_args
[`setTimeout()`]: timers.html#timers_settimeout_callback_delay_args
[`tls.CryptoStream`]: tls.html#tls_class_cryptostream
[`tls.SecureContext`]: tls.html#tls_tls_createsecurecontext_options
[`tls.SecurePair`]: tls.html#tls_class_securepair
[`tls.TLSSocket`]: tls.html#tls_class_tls_tlssocket
[`tls.createSecureContext()`]: tls.html#tls_tls_createsecurecontext_options
[`util._extend()`]: util.html#util_util_extend_target_source
[`util.debug()`]: util.html#util_util_debug_string
[`util.error()`]: util.html#util_util_error_strings
[`util.inspect()`]: util.html#util_util_inspect_object_options
[`util.inspect.custom`]: util.html#util_util_inspect_custom
[`util.isArray()`]: util.html#util_util_isarray_object
[`util.isBoolean()`]: util.html#util_util_isboolean_object
[`util.isBuffer()`]: util.html#util_util_isbuffer_object
[`util.isDate()`]: util.html#util_util_isdate_object
[`util.isError()`]: util.html#util_util_iserror_object
[`util.isFunction()`]: util.html#util_util_isfunction_object
[`util.isNull()`]: util.html#util_util_isnull_object
[`util.isNullOrUndefined()`]: util.html#util_util_isnullorundefined_object
[`util.isNumber()`]: util.html#util_util_isnumber_object
[`util.isObject()`]: util.html#util_util_isobject_object
[`util.isPrimitive()`]: util.html#util_util_isprimitive_object
[`util.isRegExp()`]: util.html#util_util_isregexp_object
[`util.isString()`]: util.html#util_util_isstring_object
[`util.isSymbol()`]: util.html#util_util_issymbol_object
[`util.isUndefined()`]: util.html#util_util_isundefined_object
[`util.log()`]: util.html#util_util_log_string
[`util.print()`]: util.html#util_util_print_strings
[`util.puts()`]: util.html#util_util_puts_strings
[`util.types`]: util.html#util_util_types
[`util`]: util.html
[`worker.exitedAfterDisconnect`]: cluster.html#cluster_worker_exitedafterdisconnect
[`zlib.bytesWritten`]: zlib.html#zlib_zlib_byteswritten
[alloc]: buffer.html#buffer_class_method_buffer_alloc_size_fill_encoding
[alloc_unsafe_size]: buffer.html#buffer_class_method_buffer_allocunsafe_size
[from_arraybuffer]: buffer.html#buffer_class_method_buffer_from_arraybuffer_byteoffset_length
[from_string_encoding]: buffer.html#buffer_class_method_buffer_from_string_encoding
[NIST SP 800-38D]: http://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-38d.pdf
[`REPLServer.clearBufferedCommand()`]: repl.html#repl_replserver_clearbufferedcommand
