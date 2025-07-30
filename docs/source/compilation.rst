编译环境
===========

不同于大多数 Linux 发行版，macOS 很早就不再采用 ``gcc`` 作为默认的 C 编译器。默认的编译器是 ``clang``，需要安装 Command Line Tools 或者 XCode （同时集成了 Command Line Tools）才可使用。XCode 可以从 App Store 或者 Apple 开发者网站下载，Command Line Tools 可从开发者网站下载或者通过 ``xcode-select --install`` 命令安装。

Command Line Tools 集成了一系列 Unix-style 的工具，例如 ``clang``, ``ld``, ``objdump``, ``ar``, ``as``, 等等，具体可见 Developer 目录（一般在 ``/Library/Developer/CommandLineTools/usr/bin``）。

.. autosummary::
   :toctree: generated

   lumache
