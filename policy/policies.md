
<!--introduced_in=v11.8.0-->
<!-- type=misc -->

> Stability: 1 - Experimental

<!-- name=policy -->

Node.js contains experimental support for creating policies on loading code.

Policies are a security feature intended to allow guarantees
about what code Node.js is able to load. The use of policies assumes
safe practices for the policy files such as ensuring that policy
files cannot be overwritten by the Node.js application by using
file permissions.

A best practice would be to ensure that the policy manifest is read only for
the running Node.js application, and that the file cannot be changed
by the running Node.js application in any way. A typical setup would be to
create the policy file as a different user id than the one running Node.js
and granting read permissions to the user id running Node.js.

