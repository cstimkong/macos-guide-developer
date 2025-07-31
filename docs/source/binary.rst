二进制文件格式
==============

``Mach-O`` 格式
---------------

Mach-O 是 macOS 中的 Object 文件格式 (对应 Linux 和 BSD 中的 ELF 文件)。

.. _binary_dynamic_lib:

动态链接库 (``.dylib``)
----------------

``Mach-O`` 文件中的动态链接库可以对应 ELF 文件类型中的 Shared Object (文件扩展名一般为 ``.so`` )。 ``Mach-O`` 文件中有两种动态链接库: ``dylib``  和 ``bundle`` ( 不同于目录结构的 Bundle)。 ``bundle`` 类型的文件扩展名可以为 ``.bundle`` (但是容易和目录结构的 Bundle 混淆) 或者直接使用 ``.so`` 。 

``dylib`` 和 ``bundle`` 的实际差别非常小, 在动态加载时有细微差别。此外, ``dylib`` 一般会被公开使用, 而 ``bundle`` 一般只在一个 app 内部使用。

可以用以下命令构建 ``dylib`` :

.. code-block:: console

    clang -dynamiclib -undefined dynamic_lookup -o libfoo.dylib foo.c

可以用以下命令构建 ``bundle``:

.. code-block:: console

    clang -bundle -undefined dynamic_lookup -o libfoo.so foo.c


.. _binary_bundle:

Bundle (App, Framework 和 Plug-in)
----------------

Bundle 是 macOS 和 iOS 中打包和分发软件的一种方式（一个 Bundle 实质上就是一个目录）。

主要有 3 种 Bundle:

* Application, 一个 macOS 应用程序就是这种类型的 Bundle (``/Applications`` 目录中的那些 ``.app``)。该类型的 Bundle 的典型结构如下:

.. code-block:: console

    MyApp.app/
        Contents/
            Info.plist
            MacOS/
            Resources/

其中, ``MacOS`` 目录中包含具体的可执行文件 (一般和 ``.app`` 目录同名), ``Info.plist`` 包含该 Bundle 的一些基本信息, ``Resources`` 包含资源文件。

* Framework, 可以视为动态链接库的进一步封装。一个典型的动态链接库的结构如下 (以 Python 为例, Python 可以从 `Python.org`_ 下载, 并安装到 ``/Library/Frameworks/Python.framework`` ):

.. _Python.org: https://www.python.org

.. code-block:: console

    Python.framework
        Python -> Versions/Current/Python
        Versions
            Current -> 3.11
            3.11
                Python
                bin
                    python3.11
                    python3.11-config
                    pip3.11
                    ...
                lib
                    python3.11
                        argparse.py
                        ast.py
                        ...
                etc
                share
                ...
                

可以看到, 一个 Framework 可以包含多个版本 (``Versions`` 的各个子目录都是一个版本), ``Versions/Current`` 是一个符号链接, 指向当前版本, ``Versions/{ver}/Python`` 是实际的动态链接库, 对应 ``libpython3.11.so`` (Linux) 或者 ``libpython3.11.dylib`` (macOS) 如果不选择构建为 Framework。 调用 Python 解释器的程序会链接到这个库。一般来说, 动态链接库的名字 (这里是 ``Python``) 和 Framework 目录名相同（可以由 ``Versions/Current/Resources/Info.plist`` 中的 ``CFBundleExecutable`` 选项指定）。

同时这个 Framework 中还包含了其他内容, 例如 Python 的可执行文件以及一些文档。很明显, Framework 比较适合 Python 的打包分发。

一个 Framework 往往被包含在一些 ``App`` Bundle 中, 作为应用程序本身的依赖。例如 Visual Studio Code 的目录结构:

.. code-block:: console

    Visual Studio Code.app
        Contents
            MacOS
                Electron
            Frameworks
                Electron Framework.framework
                Mantle.framework
                Squirrel.framework
                ...
            Resources
            Info.plist

Visual Studio Code 由 Electron 构建。实际可执行文件为 Electron (由 ``Info.plist`` 指定)。很显然，该可执行文件应该链接到 Electron Framework。
            
* Plug-in, 结构和 Application Bundle 基本一致。 不同之处是 ``MacOS`` 目录下是一个动态链接库。Bundle 目录的扩展名没有限制, 但一般是 ``.bundle`` 或者 ``.plugin`` 。

更多信息请见苹果开发者网站 `developer.apple.com`_ 。

.. _developer.apple.com: https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/AboutBundles/AboutBundles.html
