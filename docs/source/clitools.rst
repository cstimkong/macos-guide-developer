命令行工具
===========


Apple 提供了一套 Command Line Tools, 集成了一系列 Unix-style 的工具, 例如 ``clang``, ``clang++``, ``cpp``, ``objdump``, ``ar``, 等等, 还附带较低版本的 Python 和 Ruby。Command Line Tools 被安装在开发者目录 (Developer Directory, 一般在 ``/Library/Developer/CommandLineTools``)。 Command Line Tools 可从开发者网站下载, 或者通过 ``xcode-select --install`` 命令安装。

Xcode app 也集成了一套 Command Line Tools, 一般位于 ``/Applications/Xcode.app/Contents/Developer``

注意, ``/usr/bin`` 目录下面仍然有相关的可执行文件，例如 ``/usr/bin/clang``, 但实际上会调用开发者工具目录中的相关命令。


开发者目录
-------------

开发者目录 (Developer Directory) 是包含一系列 Unix-style tools。macOS 支持多个开发者目录，但只能有一个处于活动状态, 默认情况下 ``/usr/bin`` 中的相关可执行文件会调用该开发者目录中的工具。

可以使用 ``xcode-select --switch <developer directory>`` 命令切换开发者目录。 ``xcode-select --print-path`` 命令会输出当前活动的开发者目录。


开发者目录的结构
---------

以 ``/Library/Developer/CommandLineTools`` 为例,

* ``Library`` 目录内是和 Command Line Tools 有关的 Frameworks 和其他文件。

* ``usr`` 目录下包含 ``bin``, ``include``, ``libexec``, ``lib`` 和 ``share``。熟悉 Linux 的用户应该对这些目录非常熟悉。例如, ``usr/bin`` 目录内包含了各种编译构建工具, 如 ``clang``, ``clang++``, ``ld``, 等等。


Command Line Tools 中提供的工具
----------------

Command Line Tools 中提供了大量的实用工具, 主要包括:

* ``git``, Git 源代码管理工具。

* ``clang`` 和 ``clang++``, C 和 C++ 编译器。

* ``swiftc``, Swift 编译器。

* ``lldb``, LLDB 调试器。

* ``libtool`` 和 ``ranlib``, Libtool 链接库处理工具。

* ``yacc`` ( ``bison`` ), GNU Parser 生成器。

* Python 可执行文件, 包括 ``python3``, ``pydoc3``, ``pip3``, ``2to3`` 等 (Python  较老的版本)。

* LLVM 二进制工具, 包括 ``otool``, ``objdump``, ``llvm-cov`` 等。

* Apple 提供的二进制工具, 包括 ``strings``, ``size``, ``nm``, ``ld``, ``ar``, ``as`` 等。

* ``m4``, `GNU M4`_ 宏处理器 (版本较老)。

* ``make``, `GNU Make`_ (版本较老)。

* ``codesign``, Mach-O 文件代码签名工具。

* ``install_name_tool``, Mach-O 链接信息修改工具。

* ``notarytool``, macOS App 公证工具 (见 `开发者网站`_ )。

* ``stapler``, 获取公证 Tickets 的工具。


.. _GNU Make: https://www.gnu.org/software/make/

.. _GNU M4: https://www.gnu.org/software/m4/

.. _开发者网站: https://developer.apple.com/documentation/security/notarizing-macos-software-before-distribution

