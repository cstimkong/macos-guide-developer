编译环境
===========

不同于大多数 Linux 发行版，macOS 很早就不再采用 GNU 的编译构建工具, 例如 ``gcc``。默认的编译器是 ``clang``，需要安装 Command Line Tools 或者 XCode （同时集成了 Command Line Tools）才可使用。XCode 可以从 App Store 或者 Apple 开发者网站下载，Command Line Tools 可从开发者网站下载或者通过 ``xcode-select --install`` 命令安装。

Command Line Tools 集成了一系列 Unix-style 的工具, 例如 ``clang``, ``ld``, ``objdump``, ``ar``, ``as``, 等等 (还附带较低版本的 Python 和 Ruby 等)，具体可见 Developer 目录（一般在 ``/Library/Developer/CommandLineTools/usr/bin``）。注意, ``/usr/bin`` 目录下面仍然有相关的可执行文件，例如 ``/usr/bin/clang``, 但实际上会调用开发者工具目录中的相关命令。


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

Command Line Tools 中提供的工具
----------------

Command Line Tools 中提供了大量的实用工具, 主要包括:

* ``git``, Git 源代码管理工具。

* ``clang`` 和 ``clang++``, C 和 C++ 编译器。

* ``swiftc``, Swift 编译器。

* ``lldb``, LLDB 调试器。

* ``libtool`` 和 ``ranlib``, Libtool 链接库处理工具。

* ``yacc`` ( ``bison`` ), GNU Parser 生成器。

* ``python``, Python 3 较老的版本。

* LLVM 二进制工具, 包括 ``otool``, ``objdump``, ``llvm-cov`` 等。

* Apple 提供的二进制工具, 包括 ``strings``, ``size``, ``nm``, ``ld``, ``ar``, ``as``等。

* ``m4``, `GNU M4`_ 宏处理器 (版本较老)。

* ``make``, `GNU Make`_ (版本较老)。

* ``codesign``, Mach-O 文件代码签名工具。

* ``install_name_tool``, Mach-O 链接信息修改工具。

* ``notarytool``, macOS App 公证工具 (见 `开发者网站`_ )。

* ``stapler``, 获取公证 Tickets 的工具。


.. _GNU Make: https://www.gnu.org/software/make/

.. _GNU M4: https://www.gnu.org/software/m4/

.. _开发者网站: https://developer.apple.com/documentation/security/notarizing-macos-software-before-distribution


macOS SDK 中提供的库
----------------

最近版本的 macOS 15 SDK 提供了以下的自带库:

* ``libz``, 用于压缩的函数库。

* ``libxslt``, XSLT 的实现。

* ``libxml2``, 解析 XML 文档的函数库。

* ``liby``, yacc (bison) 链接库。

* ``libxar``, 解析 XAR 文档的函数库。

* ``libtcl``, Tcl 链接库 (仅为兼容性保留)。

* ``libtk``, Tk 链接库 (仅为兼容性保留)。

* ``libSystem``, 底层 C 函数库, 类似 ``glibc`` 中的 ``libc.so`` 。包含了 ``libm``, ``libpthread``, ``libc``, ``libdl`` 等基础库的实现。

* ``libc++``, Libc++ 函数库 (Linux 常用 ``libstdc++`` )。

* ``libldap`` 和 ``liblber``, LDAP 协议有关的函数库 (Linux 常用 ``openldap`` )。

* ``libsqlite3``, 用于访问 SQLite 3 数据库的函数库。

* ``libedit``, BSD Line Editting Library, 命令行编辑工具 (Linux 常用 ``libreadline`` )。

* ``libiconv``, 字符编码转换库。注意, Linux 下 glibc 包含了 ``libiconv`` 的实现, 因此不需要手动链接 ``libiconv`` 。macOS ``libiconv`` 库中的导出符号和 GNU libiconv 的也有区别, 例如: macOS ``libiconv`` 中的 ``iconv_open`` 对应 GNU libiconv 中的 ``libiconv_open`` 。为保证兼容, 头文件中进行了对应的宏定义处理。


* ``libexpat``, 面向流的 XML 解析库。

* ``libresolv``, DNS (Domain Name Service) 信息处理库, 对应 glibc 中的 ``libresolv.so`` 。

* ``libcurl``, CURL 库 (用于URL 传输)。

* ``libffi``, 外部函数接口 (Foreign Function Interface) 库。

* ``libpcap``, 网络数据包捕获函数库。

