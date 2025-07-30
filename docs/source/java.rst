Java
================

在 macOS 的 ``/usr/bin`` 目录中已经有相关的可执行文件, 如 ``java``, ``javac``, ``javap``, ``jconsole`` 等, 但是这些程序的作用是调用真正的 ``JAVA_HOME`` 目录中的对应的程序。

JDK 安装在 ``/Library/Java/JavaVirtualMachines`` 目录下。一个 JDK 被打包为一个 Bundle (见 :ref:`binary_bundle` ), 其子目录 ``Contents/Home`` 为实际的 JAVA_HOME。

一个 JDK 的典型结构如下所示:

.. code-block:: console

    jdk-21.jdk
        Contents
            MacOS
                libjli.dylib
            Info.plist
            Home
                bin
                    java
                    javac
                    javadoc
                    javap
                    ...
                jmods
                    java.base.jmod
                    java.compiler.jmod
                    ...
                lib
                include
                ...

在执行 ``/usr/bin`` 目录内的 Java 有关程序时, 会先定位具体的 JDK (如果 ``JAVA_HOME`` 环境变量已经设置, 则运行 JAVA_HOME 目录内的相关工具), 如果没有设置 JAVA_HOME 则在已经安装的 JDK 中寻找最合适的 JAVA_HOME (通过 ``/usr/libexec/java_home`` )。