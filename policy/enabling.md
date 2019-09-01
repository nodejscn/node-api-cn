
<!-- type=misc -->

The `--experimental-policy` flag can be used to enable features for policies
when loading modules.

Once this has been set, all modules must conform to a policy manifest file
passed to the flag:

```sh
node --experimental-policy=policy.json app.js
```

The policy manifest will be used to enforce constraints on code loaded by
Node.js.

To mitigate tampering with policy files on disk, an integrity for
the policy file itself may be provided via `--policy-integrity`.
This allows running `node` and asserting the policy file contents
even if the file is changed on disk.

```sh
node --experimental-policy=policy.json --policy-integrity="sha384-SggXRQHwCG8g+DktYYzxkXRIkTiEYWBHqev0xnpCxYlqMBufKZHAHQM3/boDaI/0" app.js
```

