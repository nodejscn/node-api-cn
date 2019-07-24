
<!-- type=misc -->

The `--experimental-modules` flag can be used to enable support for
ECMAScript modules (ES modules).

Once enabled, Node.js will treat the following as ES modules when passed to
`node` as the initial input, or when referenced by `import` statements within
ES module code:

- Files ending in `.mjs`.

- Files ending in `.js`, or extensionless files, when the nearest parent
  `package.json` file contains a top-level field `"type"` with a value of
  `"module"`.

- Strings passed in as an argument to `--eval` or `--print`, or piped to
  `node` via `STDIN`, with the flag `--input-type=module`.

Node.js will treat as CommonJS all other forms of input, such as `.js` files
where the nearest parent `package.json` file contains no top-level `"type"`
field, or string input without the flag `--input-type`. This behavior is to
preserve backward compatibility. However, now that Node.js supports both
CommonJS and ES modules, it is best to be explicit whenever possible. Node.js
will treat the following as CommonJS when passed to `node` as the initial input,
or when referenced by `import` statements within ES module code:

- Files ending in `.cjs`.

- Files ending in `.js`, or extensionless files, when the nearest parent
  `package.json` file contains a top-level field `"type"` with a value of
  `"commonjs"`.

- Strings passed in as an argument to `--eval` or `--print`, or piped to
  `node` via `STDIN`, with the flag `--input-type=commonjs`.

