编译环境
===========

不同于大多数 Linux 发行版，macOS 很早就不再采用 GNU 的编译构建工具, 例如 ``gcc``。默认的编译器是 ``clang``，需要安装 Command Line Tools 或者 XCode （同时集成了 Command Line Tools）才可使用。XCode 可以从 App Store 或者 Apple 开发者网站下载，Command Line Tools 可从开发者网站下载或者通过 ``xcode-select --install`` 命令安装。

Command Line Tools 集成了一系列 Unix-style 的工具, 例如 ``clang``, ``ld``, ``objdump``, ``ar``, ``as``, 等等（还附带较低版本的 Python 和 Ruby 等），具体可见 Developer 目录（一般在 ``/Library/Developer/CommandLineTools/usr/bin``）。注意, ``/usr/bin`` 目录下面仍然有相关的可执行文件，例如 ``/usr/bin/clang``, 但实际上会调用开发者工具目录中的相关命令。

活动的开发者目录
-------------

开发者目录 (Developer Directory) 是包含一系列 Unix-style tools 的根目录。可以安装多个开发者目录，但只能有一个处于活动状态, 默认情况下会调用该开发者目录中的工具。

Xcode 的开发者目录一般位于 ``/Applications/Xcode.app/Contents/Developer``。如果 macOS 中安装了多个版本的 Xcode, 就有多个这样的开发者目录。另外使用 ``xcode-select --install`` 安装的开发者目录位于 ``/Library/Developer/CommandLineTools``。

可以使用 ``xcode-select --switch <developer directory>`` 命令切换开发者目录。 ``xcode-select --print-path`` 命令会输出当前活动的开发者目录。


开发者目录的结构
---------

以 ``/Library/Developer/CommandLineTools`` 为例,

* ``Library`` 目录内是和 Command Line Tools 有关的 Frameworks 和其他文件。

* ``usr`` 目录下包含 ``bin``, ``include``, ``libexec``, ``lib`` 和 ``share``。熟悉 Linux 的用户应该对这些目录非常熟悉。例如, ``usr/bin`` 目录内包含了各种编译构建工具, 如 ``clang``, ``clang++``, ``ld``, 等等。

* ``SDK`` 目录内是 Command Line Tools 附带的 SDK (默认为 ``MacOSX.sdk`` )。具体的 SDK 目录内仍然还有一个 ``usr`` 目录。该目录的内容是具体的头文件和和可供链接的动态链接库 (注意，较早期版本的 macOS,头文件仍可以在 ``/usr/include`` 中找到, 但是现在的一些通用头文件只能在 SDK 目录中找到)。SDK 目录中的 ``usr`` 目录包含了 ``bin``, ``include``, ``lib`` 等熟知的子目录。 ``usr/include`` 中包含了真正可供引入的头文件，例如 ``stdio.h``, ``stdlib.h``, ``unistd.h``，等等。 ``usr/lib`` 目录中包含了动态链接库 (现在的 SDK 会以 ``.tbd`` 文件的形式提供)。

.. autosummary::
   :toctree: generated

   lumache
