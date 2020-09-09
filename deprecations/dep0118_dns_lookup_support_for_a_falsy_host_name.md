<!-- YAML
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/23173
    description: Runtime deprecation.
-->

Type: Runtime

Previous versions of Node.js supported `dns.lookup()` with a falsy host name
like `dns.lookup(false)` due to backward compatibility.
This behavior is undocumented and is thought to be unused in real world apps.
It will become an error in future versions of Node.js.

