macOS 目录结构
===============

macOS 的目录结构和一般的 Unix-like 系统类似, 但是有很多特有的目录。

主要目录
----------------


* ``/Applications`` 目录: 包含安装的应用程序 ( ``.app`` Bundle)。 macOS 自带的 apps 在 ``/System/Applications`` 目录中。

* ``/usr/lib`` 目录: 现在的 macOS 已经将大部分动态链接库放置在 dyld cache 中, ``/usr/lib`` 目录中不可见。

* ``/usr/bin`` 目录: 包含自带的工具类可执行文件。

* ``/usr/libexec`` 目录: 包含不是直接由用户执行的可执行文件。

* ``/usr/local`` 目录: 用户可以自由写入, 作用和其他类 Unix 操作系统中的对应目录一致。

* ``/bin`` 目录: 包含日常经常使用的可执行文件。

* ``/Users`` 目录: 包含用户主目录的根目录。

* ``/Library`` 目录: 包含各种应用程序的资源文件 (System Level)。

* ``/System`` 目录: 包含 macOS 系统的核心资源文件。

  * ``/System/Applications``: 包含 Apple 自带的 apps。

  * ``/System/Library``: 包含 Apple 自带的 apps 有关的核心资源文件。

  * ``/System/Volumes``: 包含 APFS 文件系统中特殊 Volumes 的挂载点。


可写的目录
----------------------


注意, 在现在的 macOS 中, ``/usr`` 目录中除了 ``local`` 子目录以及 ``libexec/cups`` 等少部分目录外, 其他的目录都是不可写的 (自 macOS 10.15 开始)。

其他可写的目录还包括:

* ``/opt``, 作用和 Linux 中 ``/opt`` 目录相同。

* ``/Users``, 作用相当于 Linux 中的 ``/home`` 目录。

* ``/etc`` (实际指向 ``/private/etc`` ), 相当于 Linux 中的 ``/etc`` 目录。

* ``/tmp`` (实际指向 ``/private/tmp``), 相当于 Linux 中的 ``/tmp`` 目录。

* ``/var`` (实际指向 ``/private/var``), 相当于 Linux 中的 ``/var`` 目录。

* ``/Applications``, 包含用户自己安装的应用程序 (注意, Launch pad 中显示的应用程序还有来自 ``/System/Applications`` 的, 如 ``Safari.app`` 等 Apple 自己开发的 apps)。

除了 ``/opt``, ``/usr/local``, 其他目录仍然受限于 System Integrity Protection (SIP) 的保护, 部分文件无法被修改和删除。

macOS Volume 分析
---------------------

从 macOS Volume 角度分析, 一个 macOS 实例安装在一个 APFS Container 中, 这个 Container 至少包含了以下 Volumes:

* ``Macintosh HD`` 卷: 这是包含 macOS 系统核心文件的 Volume。 该 Volume 的一个 snapshot 会被挂载为根目录 ``/`` , 因此根目录实际上是只读的。

* ``Data`` 卷: 这是 包含 macOS 可修改数据的 Volume。 该 Volume 会被挂载到 ``/System/Volumes/Data`` 。该 Volume 和 ``Macintosh HD`` 卷形成一个 Volume Group。 该卷中的部分目录会形成在 ``Macintosh HD`` 卷中的 firmlink, 例如 ``/usr/local`` ( ``/usr/local`` 和 ``/System/Volumes/Data/usr/local`` 的 inode ID 一致)。 因此, 可以直接通过 ``/usr/local`` 访问到 ``Data`` 卷中对应目录的内容。

* ``Recovery``, ``Preboot`` 和 ``VM`` 卷: 用于操作系统 recovery 等功能, 具体情况没有公开。

APFS 卷的信息可以通过 ``diskutil`` 命令查看。