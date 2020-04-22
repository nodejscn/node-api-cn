
V8 has its own set of CLI options. Any V8 CLI option that is provided to `node`
will be passed on to V8 to handle. V8's options have _no stability guarantee_.
The V8 team themselves don't consider them to be part of their formal API,
and reserve the right to change them at any time. Likewise, they are not
covered by the Node.js stability guarantees. Many of the V8
options are of interest only to V8 developers. Despite this, there is a small
set of V8 options that are widely applicable to Node.js, and they are
documented here:

