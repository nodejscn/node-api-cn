
Unlike modules written in JavaScript, developing and deploying Node.js
native addons using N-API requires an additional set of tools. Besides the
basic tools required to develop for Node.js, the native addon developer
requires a toolchain that can compile C and C++ code into a binary. In
addition, depending upon how the native addon is deployed, the *user* of
the native addon will also need to have a C/C++ toolchain installed.

For Linux developers, the necessary C/C++ toolchain packages are readily
available. [GCC][] is widely used in the Node.js community to build and
test across a variety of platforms. For many developers, the [LLVM][]
compiler infrastructure is also a good choice.

For Mac developers, [Xcode][] offers all the required compiler tools.
However, it is not necessary to install the entire Xcode IDE. The following
command installs the necessary toolchain:

```bash
xcode-select --install
```

For Windows developers, [Visual Studio][] offers all the required compiler
tools. However, it is not necessary to install the entire Visual Studio
IDE. The following command installs the necessary toolchain:

```bash
npm install --global --production windows-build-tools
```

The sections below describe the additional tools available for developing
and deploying Node.js native addons.

