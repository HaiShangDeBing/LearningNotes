# Java

[TOC]

## 概述

Java是一门纯粹的面相对象编程语言，吸收了 C++ 语言的各种优点，又摒弃了 C++ 里难以理解的多继承、指针等概念。

它既具有解释型语言的特征，也具有编译型语言的特征，需要经过先编译，后解释两个步骤。

### 高级语言的运行机制

计算机高级语言按程序的执行方式可以分为编译型和解释型两种。

编译型语言是指用专门的编译器，针对特定平台（操作系统）将某种高级语言源代码一次性翻译成可被该平台硬件执行的机器码，并包装成该平台所能识别的可执行性程序的格式，这个转换过程称为编译。编译生成的可执行性程序可以脱离开发环境，在特定的平台上独立运行。

解释型语言是指使用专门的解释器对源程序逐行解释成特定平台的机器码并立即执行的语言。解释型语言通常不会进行整体性的编译和链接处理，解释型语言相当于把编译型语言中的编译和解释过程混合到一起同时完成。每次执行解释型语言的程序都需要进行一次编译，因此解释型语言的程序运行效率通常较低，而且不能脱离解释器独立运行。但解释型语言有一个优势：跨平台比较容易，只需提供后特定平台的解释器即可。

### Java程序的运行机制

Java的编译步骤并不会生成特定平台的机器码，而是生成一种与平台无关的字节码（也就是*.class文件）。这种字节码不是可执行性的，必须使用Java解释器来解释执行。

Java	负责解释执行字节码文件的是Java虚拟机（JVM），所有平台上的JVM想编译器提供相同的编程接口，而编译器只需面向虚拟机。

JVM是一个抽象的计算机，和实际的计算机一样，它具有指令集并使用不同的存储区域。它负责执行指令，还要管理数据、内存和寄存器。

Java运行时环境（JRE）它是运行Java程序的必需条件。JRE包括核心API、集成API、用户界面API、发布技术、JVM。

JDK包括编译Java程序的编译器（javac）。

### Java垃圾回收机制

与C/C++程序不同，Java语言不需要程序员直接控制内存回收，Java程序的内存分配和回收都是由JRE在后台自动进行的。通常JRE会提供一个后台线程来进行检测和控制，一般都是在CPU空闲或内存不足时自动进行垃圾回收，而程序员无法精确控制垃圾回收的时间和顺序等。

垃圾回收机制可以很好地提高编程效率，保护程序的完整性。

垃圾回收机制只能回收内存资源，对其他物理资源，如数据库链接、磁盘I/O等资源无能为力。为了更快回收那些不再使用的对象，可以将对象的引用变量设置为null。

### JAR文件

JAR文件（Java Archive File）,即Java档案文件，通常是一种压缩文件，与常见的ZIP压缩文件兼容。默认包含了一个名为META-INF/MANIFEST.MF清单文件。当开发了一个应用程序后，这个应用程序包含了很多类，如果需要把这个应用程序提供给别人使用，通常会将这些类文件打包成一个JAR文件。