<!-- YAML
added: v8.0.0
-->
* `label` {string}

This method does not display anything unless used in the inspector. The
`console.profile()` method starts a JavaScript CPU profile with an optional
label until [`console.profileEnd()`][] is called. The profile is then added to
the **Profile** panel of the inspector.
```js
console.profile('MyLabel');
// Some code
console.profileEnd();
// Adds the profile 'MyLabel' to the Profiles panel of the inspector.
```

