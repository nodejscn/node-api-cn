
Strings passed in as an argument to `--eval` or `--print` (or `-e` or `-p`), or
piped to `node` via `STDIN`, will be treated as ES modules when the
`--input-type=module` flag is set.

```sh
node --input-type=module --eval "import { sep } from 'path'; console.log(sep);"

echo "import { sep } from 'path'; console.log(sep);" | node --input-type=module
```

For completeness there is also `--input-type=commonjs`, for explicitly running
string input as CommonJS. This is the default behavior if `--input-type` is
unspecified.

