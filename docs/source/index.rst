写给 Linux 开发者的 macOS 指南!
===================================

本文档介绍了面向*开发者* (特别是有 Linux 使用经验)的 macOS 使用教程。虽然 Linux、FreeBSD 以及 macOS 都是 Unix-like 操作系统, 但是无论从底层内核还是上层应用的角度来看, 都有较大的不同。因此, 本文档重点介绍了macOS 中相比其他类 Unix 操作系统 (特别是 Linux) 最重要的一些特性, 以便让具备 Linux 开发经验的读者快速上手 macOS。

推荐的前置知识:

* Coreutils 中常用工具的使用 (ls, cp, mv, rm 等)。

* 了解 glibc 以及 ``binutils``, ``gcc``, ``ar``, ``as``, ``clang``, ``ld`` 等二进制处理及编译构建工具。

* 基本的 Bash 脚本编写。

* 了解 ELF 文件的结构。

* 了解 POSIX 标准中重要函数的使用 (如 fork, execve, pipe 等)。

* 了解程序的编译链接过程。

了解以下知识更佳:

* LLVM

* ``ncurses``, ``libxml2``, ``libreadline``, ``libssl`` 等常见库的使用

* x86 或 ARM 汇编

* 除了 C/C++ 之外的系统级编程语言 (如 Rust 和 Go)

这些知识并不是必需的, 但对于深刻理解本文档的内容会有帮助。


.. note::

   This project is under active development.

Contents
--------

.. toctree::
   hierarchy
   utility
   clitools
   macossdk
   binary
   java
