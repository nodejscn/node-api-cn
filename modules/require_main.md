<!-- YAML
added: v0.1.17
-->

* {Object}

The `Module` object representing the entry script loaded when the Node.js
process launched.
See ["Accessing the main module"](#modules_accessing_the_main_module).

In `entry.js` script:

```js
console.log(require.main);
```

```sh
node entry.js
```

<!-- eslint-skip -->
```js
Module {
  id: '.',
  exports: {},
  parent: null,
  filename: '/absolute/path/to/entry.js',
  loaded: false,
  children: [],
  paths:
   [ '/absolute/path/to/node_modules',
     '/absolute/path/node_modules',
     '/absolute/node_modules',
     '/node_modules' ] }
```

