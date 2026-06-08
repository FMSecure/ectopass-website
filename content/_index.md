+++
title = "Home"
menu = "main"
weight = 1
+++

## Ectopass detects micro-architectural security vulnerabilities

Current processor optimizations such as branch prediction or speculation are essential for
performance but can break security by accidentally **leaking data**. See for example the [Spectre attack](https://spectreattack.com/).

![demo screenshot](/static/images/demo.png)

### Try it in the browser

You can directly try a demo of Ectopass from your browser:

- Open [VS Code](https://vscode.dev/) for the web.
- Search for the [Ectopass](https://marketplace.visualstudio.com/items?itemName=ectopass.ectopass) extension and install it.
- Launch the `Ectopass: Demo` command.

### How Ectopass works

![ectopass architecture](/static/images/arch.png)

Ectopass is implemented as an [LLVM](https://en.wikipedia.org/wiki/LLVM) pass (hence the name). It can be integrated with any codebase which can
be compiled to LLVM IR (C, C++, Rust, Swift, etc).

Ectopass builds the Control Flow Graph of every function of the codebase, extends it with speculative paths, calculates data dependencies and then performs an analysis based on [Leakage Containment Models](https://arxiv.org/abs/2112.10511).

### Configuration

Ectopass analysis can be configured with different options:

- different kind of CPU models
- different security conditions (non-interference, conditional non-interference, relative security)
- different side channel types
- security tags (a list of untrusted variable or secrets)

### Existing solutions

![selective SLH](/static/images/slh.png)

The existing solutions are either impractical (like changing the hardware) or do not scale for big codebases (like [SLH](https://llvm.org/docs/SpeculativeLoadHardening.html)).

Ectopass can help pinpoint the exact files where vulnerabilities can be found and limit the scope of SLH to those files.
Activating SLH to all files of a project (industry default) can be very time consuming.

Benchmarking on [`libsodium`](https://github.com/jedisct1/libsodium), we observed an overhead of 831% with SLH activated on all files compared to
only **4%** when partially activating it on vulnerable files reported by Ectopass.

### Analyzing large projects

The demo available in the browser is only suitable to analyze a small C file. If you would like
to analyze larger projects with Ectopass and check if they have vulnerabilities,
please [get in touch](contact)!
