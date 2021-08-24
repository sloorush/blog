+++
title = "Intro to eBPF"
date = "2021-08-24"
author = "r-ush"
cover = "img/ebpf.png"
description = "eBPF is a revolutionary technology with origins in the Linux kernel that can run sandboxed programs in an operating system kernel."
draft = false
+++

## What is eBPF?

eBPF is a revolutionary technology with origins in the Linux kernel that can run sandboxed programs in an operating system kernel. It is used to safely and efficiently extend the kernel's capabilities without requiring to change kernel source code or load kernel modules.

Wait, what?

![ebpf basics](https://i.imgur.com/OT38RIt.png)

Today, eBPF is used extensively to drive a wide variety of use cases: Providing high-performance networking and load-balancing in modern data centres and cloud-native environments, extracting fine-grained security observability data at low overhead, helping application developers trace applications, providing insights for performance troubleshooting, preventive application and container runtime security enforcement, and much more. The possibilities are endless, and the innovation that eBPF is unlocked has only just begun.

## But why?

You'd think(at least I thought) you can already do all the stuff on Linux; why do you even need something like this but then...

before eBPF----->
![](https://isovalent.com/assets/blog/ebpf-foundation-announcement/Comic1.png)
after eBPF------>
![](https://isovalent.com/assets/blog/ebpf-foundation-announcement/Comic2.png)

A small and very relatable analogy can be like <i>eBPF doing to Linux, what javascript did to the web</i>:

### The Power of Programmability

Let's start with an analogy. Do you remember GeoCities? Twenty years ago, web pages used to be almost exclusively written in static markup language (HTML). A web page was basically a document with an application (browser) able to display it. Looking at web pages today, web pages have become full-blown applications, and web-based technology has replaced a vast majority of applications written in languages requiring compilation. What enabled this evolution?

![](https://i.imgur.com/FUImfbW.png)

The short answer is programmability with the introduction of JavaScript. It unlocked a massive revolution resulting in browsers evolving into almost independent operating systems.

Why did the evolution happen? Programmers were no longer as bound to users running particular browser versions. Instead of convincing standards bodies that a new HTML tag was needed, the availability of the necessary building blocks decoupled the pace of innovation of the underlying browser from the application running on top. This is, of course, a bit oversimplified as HTML did evolve over time and contributed to the success, but the evolution of HTML itself would not have been sufficient.

Before taking this example and applying it to eBPF, let's look at a couple of key aspects that were vital in the introduction of JavaScript:

- Safety: Untrusted code runs in the browser of the user. This was solved by sandboxing JavaScript programs and abstracting access to browser data.
- Continuous Delivery: Evolution of program logic must be possible without constantly shipping new browser versions. This was solved by providing the right low-level building blocks sufficient to build arbitrary logic.
- Performance: Programmability must be provided with minimal overhead. This was solved with the introduction of a Just-in-Time (JIT) compiler.

For all of the above, exact counterparts can be found in eBPF for the same reason.

## Development toolchain

Several development toolchains exist to assist in the development and management of eBPF programs. All of them address different needs of users:

### bcc

BCC is a framework that enables users to write python programs with eBPF programs embedded inside them. The framework is primarily targeted for use cases that involve application and system profiling/tracing where an eBPF program is used to collect statistics or generate events, and a counterpart in userspace collects the data and displays it in a human-readable form. Running the python program will generate the eBPF bytecode and load it into the kernel.
![](https://i.imgur.com/sZ9fyyR.png)

### bpftrace

bpftrace is a high-level tracing language for Linux eBPF and is available in recent Linux kernels (4.x). bpftrace uses LLVM as a backend to compile scripts to eBPF bytecode and makes use of BCC for interacting with the Linux eBPF subsystem as well as existing Linux tracing capabilities: kernel dynamic tracing (kprobes), user-level dynamic tracing (uprobes), and tracepoints. The bpftrace language is inspired by awk, C and predecessor tracers such as DTrace and SystemTap.
![](https://i.imgur.com/VslEFzm.png)

### eBPF Go Library

The eBPF Go library provides a generic eBPF library that decouples the process of getting to the eBPF bytecode and the loading and management of eBPF programs. eBPF programs are typically created by writing a higher-level language and then use the clang/LLVM compiler to compile to eBPF bytecode.
![](https://i.imgur.com/NtkM5oE.png)

### libbpf C/C++ Library

The libbpf library is a C/C++-based generic eBPF library that helps to decouple the loading of eBPF object files generated from the clang/LLVM compiler into the kernel and generally abstracts interaction with the BPF system call by providing easy to use library APIs for applications.
![](https://i.imgur.com/tNIptkT.png)

# Community

Join the slack community [here](https://ebpf.io/slack)

## Read More

- https://ebpf.io/
- https://ebpf.io/what-is-ebpf/
- https://isovalent.com/blog/post/2021-08-ebpf-foundation-announcement
- https://docs.cilium.io/en/latest/bpf/#bpf-guide
- https://github.com/cilium/
- https://github.com/feniljain/knowledge-base/tree/main/linux#ebpf
