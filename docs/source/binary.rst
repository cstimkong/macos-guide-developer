二进制文件格式
==============

``Mach-O`` 格式
---------------


动态链接库 (``.dylib``)
----------------



Bundle (App, Framework 和 Bundle)
----------------

Bundle 是 macOS 和 iOS 中打包和分发软件的一种方式（一个 Bundle 实质上就是一个目录）。

主要有 4 种 Bundle:

* App, 一个 macOS 应用程序就是这种类型的 Bundle (``/Applications`` 目录中的那些 ``.app``)。该类型的 Bundle 的典型结构如下:

.. code-block:: console

    MyApp.app/
        Contents/
            Info.plist
            MacOS/
            Resources/

其中, ``MacOS`` 目录中包含具体的可执行文件 (一般和 ``.app`` 目录同名), ``Info.plist`` 包含该 Bundle 的一些基本信息, ``Resources`` 包含资源文件。