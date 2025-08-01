常用工具
===========

本章节介绍 macOS 中常用的一些工具 (Utilities) , 在 ``/bin`` 目录中。 大部分工具都是 FreeBSD-style 的, 和 Linux 中对应工具的用法有所不同。

.. _lscommand:

命令 `ls`
------------

To use Lumache, first install it using pip:

.. code-block:: console

   (.venv) $ pip install lumache

.. _xattrcommand:

命令 `xattr`
----------------

macOS 支持文件的扩展属性 (一系列 Key-value 对), 对应 Linux 中的 `attr`_ 系列工具 ( ``attr``, ``getfattr``, ``setfattr`` ) 所提供的功能。

.. _attr: https://savannah.nongnu.org/projects/attr

典型的扩展属性包括 ``com.apple.quarantine``: 通过 Chrome 等浏览器下载的文件会被附加这个属性, 表示这个文件在隔离状态, 会受到一些限制 (比如未经签名和公证的可执行文件会被阻止运行)。

``xattr`` 命令的语法如下:

.. code-block:: console

   xattr [-lrsvx] file ...
   xattr -p [-lrsvx] attr_name file ...
   xattr -w [-rsx] attr_name attr_value file ...
   xattr -d [-rsv] attr_name file ...
   xattr -c [-rsv] file ...
   xattr -h | --help

可以通过 man 命令查看其参考文档。

.. _cpcommand:

命令 `cp`
------------

macOS 中自带的 ``cp`` 命令基本和 FreeBSD 中的 ``cp`` 相同。 用法和 Linux 中的 ``cp`` 相似, 但是有以下不同:

* 在 macOS 中 ``-r`` 相当于 ``-RL``, 即在递归复制一个目录时跟随所有的系统链接 (Follow Symlinks), 而不像Linux 中的 ``cp`` 命令, ``-r`` 和 ``-R`` 是同义词。当然, ``-r`` 参数已经不建议使用。需要复制目录时直接使用 ``-R`` 选项即可。

* 对于 macOS 的 ``cp`` 命令, 使用递归模式复制时 ( ``-R`` 选项), 如果被复制的目录以 ``/`` 结尾, 则复制目录中的内容而不是目录本身。


.. _lncommand:

命令 `ln`
-----------

和 Linux 中的 ``ln`` 基本相同, 但是要注意以下不同点:

* macOS ``ln`` 命令的 ``-L`` 选项表示在建立对一个符号链接 (Symbolic Link) 的硬链接 (Hard Link) 时, 硬链接的目标是该符号链接实际指向的路径而不是符号链接本身。 Linux ``ln`` 命令的 ``-L`` 选项并没有限制在硬链接。

* macOS ``ln`` 命令没有 ``-r`` 和 ``-P`` 和 ``-S`` 选项。

