macOS SDK
=================

macOS SDK 目录在 Developer Directory 内。SDK 目录的名称一般是 ``MacOSX.sdk``, ``MacOSX15.sdk`` 等。SDK 目录可以用作 SYSROOT 目录 (主要用作在交叉编译时指定的寻找头文件和库的根目录)。

一个典型的 SDK 目录结构如下:

.. code-block:: console

    Entitlements.plist
    SDKSettings.plist
    SDKSettings.json
    System
        Library
            Frameworks
                OpenGL.framework
                OpenDirectory.framework
                Ruby.framework
                WebKit.framework
                ...
    usr
        bin
        include
        lib
            libcurl.tbd
            libncurses.tbd
            libxml2.tbd
            liby.a
            libz.tbd
            ...
        libexec
        shared

具体的来说, SDK 的 ``usr`` 目录结构和 Linux 的非常相似。例如, ``usr/include`` 包含了一些熟知的可供引入的头文件, 如 ``unistd.h``, ``stdio.h``, ``dlfcn.h`` 等等。主要区别在于, ``usr/lib`` 中包含的是 ``.tbd`` 形式的动态链接库, 而不是实际的库 (在现在的 macOS 中, 这些库已经被置于 dyld cache 中)。

``System/Library/Frameworks`` 目录中包含了 macOS 中可供链接的 frameworks。一个 framework 中的动态链接库以 ``.tbd`` 文件的形式存在。 注意, macOS 的 ``/System/Library/Frameworks`` 目录中也有这些 frameworks, 但是 frameworks 内实际的动态链接库是不存在的 (同样被置于 dyld cache 中)。 关于 framework 的更多信息, 可以参考 :ref:`binary_bundle` 。

macOS SDK 中提供的库
----------------

最近版本的 macOS 15 SDK 提供了以下的自带库:

* ``libz``, 用于压缩的函数库。

* ``libxslt``, XSLT 的实现。

* ``libxml2``, 解析 XML 文档的函数库。

* ``liby``, `GNU Bison`_ (yacc) 链接库。

* ``libxar``, 解析 XAR 文档的函数库。

* ``libtcl``, Tcl 链接库 (仅为兼容性保留)。

* ``libtk``, Tk 链接库 (仅为兼容性保留)。

* ``libSystem``, 底层 C 函数库, 可以对应 ``libc.so`` 以及 ``libm.so``, ``libpthread.so``, ``libdl.so`` 等 glibc 中的动态链接库。

* ``libc++``, Libc++ 函数库 (Linux 常用 ``libstdc++`` )。

* Ncurses 函数库, 包括 ``libncurses``, ``libform``, ``libpanel``, ``libmenu``, 对应 Linux 中的 ``ncurses`` 和 ``ncursesw`` 。

* ``libldap`` 和 ``liblber``, LDAP 协议有关的函数库 (Linux 常用 ``openldap`` )。

* ``libsqlite3``, 用于访问 SQLite 3 数据库的函数库。

* ``libedit``, `BSD Line Editting Library`_, 命令行编辑工具 (Linux 常用 `libreadline`_ )。

* ``libiconv``, 字符编码转换库。注意, Linux 下 glibc 包含了 ``libiconv`` 的实现, 因此不需要手动链接 ``libiconv`` 。macOS ``libiconv`` 库中的导出符号和 GNU libiconv 的也有区别, 例如: macOS ``libiconv`` 中的 ``iconv_open`` 对应 GNU libiconv 中的 ``libiconv_open`` 。为保证兼容, 头文件中进行了对应的宏定义处理。

* ``libexpat``, 面向流的 XML 解析库。

* ``libresolv``, DNS (Domain Name Service) 信息处理库, 对应 glibc 中的 ``libresolv.so`` 。

* ``libcurl``, CURL 库 (用于URL 传输)。

* ``libffi``, 外部函数接口 (Foreign Function Interface) 库。

* ``libpcap``, 网络数据包捕获函数库。

* ``libkrb4``, ``libkrb5``, `Kerberos 协议`_ 的函数库。

.. _BSD Line Editting Library: https://thrysoee.dk/editline/

.. _libreadline: https://tiswww.case.edu/php/chet/readline/

.. _Kerberos 协议: https://web.mit.edu/kerberos/

.. _GNU Bison: https://www.gnu.org/software/bison/

以上的库在主流 Linux 发行版中均有对应的选项, 可以通过 apt 或者 yum 等包管理器安装。