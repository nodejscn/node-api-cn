
The `"import"`, `"require"`, `"node"` and `"default"` conditions are defined
and implemented in Node.js core,
[as specified above](#esm_conditional_exports).

Other condition strings are unknown to Node.js and thus ignored by default.
Runtimes or tools other than Node.js can use them at their discretion.

These user conditions can be enabled in Node.js via the [`--conditions`
flag](#packages_resolving_user_conditions).

The following condition definitions are currently endorsed by Node.js:

* `"browser"` - any environment which implements a standard subset of global
   browser APIs available from JavaScript in web browsers, including the DOM
   APIs.
* `"development"` - can be used to define a development-only environment
   entry point. _Must always be mutually exclusive with `"production"`._
* `"production"` - can be used to define a production environment entry
   point. _Must always be mutually exclusive with `"development"`._

The above user conditions can be enabled in Node.js via the [`--conditions`
flag](#packages_resolving_user_conditions).

Platform specific conditions such as `"deno"`, `"electron"`, or `"react-native"`
may be used, but while there remain no implementation or integration intent
from these platforms, the above are not explicitly endorsed by Node.js.

New conditions definitions may be added to this list by creating a PR to the
[Node.js documentation for this section][]. The requirements for listing a
new condition definition here are that:

* The definition should be clear and unambiguous for all implementers.
* The use case for why the condition is needed should be clearly justified.
* There should exist sufficient existing implementation usage.
* The condition name should not conflict with another condition definition or
  condition in wide usage.
* The listing of the condition definition should provide a coordination
  benefit to the ecosystem that wouldn't otherwise be possible. For example,
  this would not necessarily be the case for company-specific or
  application-specific conditions.

The above definitions may be moved to a dedicated conditions registry in due
course.

