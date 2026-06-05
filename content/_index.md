+++
#title = "Home"
menu = "main"
weight = 1
+++

Current processor optimizations such as branch prediction or speculation are essential for
performance but can break security by accidentaly **leaking data**. See [Spectre](https://spectreattack.com/).

Ectopass lets you analyze your program to detect and mitigate microarchitectural security vulnerabilities.

Try it [here](#Demo)!

### Existing solutions

The existing solutions are either impractical (like changing the hardware) or do not scale for big codebases (like [SLH](https://llvm.org/docs/SpeculativeLoadHardening.html)).

### How Ectopass works

Etopass is implemented as an LLVM pass (hence the name). It can be used with any codebase which can
be compiled to LLVM IR.
Ectopass builds the Control Flow Graph of every function of the codebase, extends it with speculative paths, calculates data dependencies and then performs an analysis based on [Leakage Containment Models](https://arxiv.org/abs/2112.10511).

### Configuration

Ectopass analysis can be configured with different options:

* different kind of CPU models
* different security conditions (non-interference, conditional non-interference, relative security)
* different side channel types
* security tags (a list of untrusted variable or secrets)

### Benchmarking

Ectopass can help pinpoint the exact files where vulnerabilities can be found and limit the scope of SLH to those files.
Activating SLH to all files of a project (industry default) can be very time consuming.

Benchmarking on `libsodium`, we observed an overhead of 831% with SLH activated on all files compared to
only 4% when partially activating it on vulnerable files reported by Ectopass.

### Try it

You can directly try a demo of Ectopass from your browser:

* Open [VSCode](https://vscode.dev/) for the web.
* Search for the [Ectopass](https://marketplace.visualstudio.com/items?itemName=ectopass.ectopass) extension and install it.
* Launch the "Ectopass: Demo" command.
