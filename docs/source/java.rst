Java
================

在 macOS 的 ``/usr/bin`` 目录中已经有相关的可执行文件, 如 ``java``, ``javac``, ``javap``, ``jconsole`` 等, 但是这些程序的作用是调用真正的 ``JAVA_HOME`` 目录中的对应的程序。

JDK 安装在 ``/Library/Java/JavaVirtualMachines`` 目录下。一个 JDK 被打包为一个 Bundle (见 :ref:`binary_bundle` ), 其子目录 ``Contents/Home`` 为实际的 JAVA_HOME。