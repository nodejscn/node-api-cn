
| Feature | Reason |
| --- | --- |
| `require('./foo.mjs')` | ES Modules have differing resolution and timing, use language standard `import()` |
| `import()` | pending newer V8 release used in Node.js |
| `import.meta` | pending V8 implementation |
| Loader Hooks | pending Node.js EP creation/consensus |

