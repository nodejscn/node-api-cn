
Dynamic `import()` is supported in both CommonJS and ES modules. It can be used
to include ES module files from CommonJS code.

```js
(async () => {
  await import('./my-app.mjs');
})();
```

