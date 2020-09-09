
[Section 8.7][] of the [ECMAScript Language Specification][] defines the concept
of an "Agent" as a self-contained environment in which JavaScript code runs.
Multiple such Agents may be started and terminated either concurrently or in
sequence by the process.

A Node.js environment corresponds to an ECMAScript Agent. In the main process,
an environment is created at startup, and additional environments can be created
on separate threads to serve as [worker threads][]. When Node.js is embedded in
another application, the main thread of the application may also construct and
destroy a Node.js environment multiple times during the life cycle of the
application process such that each Node.js environment created by the
application may, in turn, during its life cycle create and destroy additional
environments as worker threads.

From the perspective of a native addon this means that the bindings it provides
may be called multiple times, from multiple contexts, and even concurrently from
multiple threads.

Native addons may need to allocate global state which they use during
their entire life cycle such that the state must be unique to each instance of
the addon.

To this end, N-API provides a way to allocate data such that its life cycle is
tied to the life cycle of the Agent.

