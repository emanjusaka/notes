## 输入和输出-源和目标

​	术语输入输出有时可能会让人混淆。应用程序一部分的输入通常是另一部分的输出。OutputStream是输出被写入的流，还是输出来自（供您读取）的流？毕竟，InputStream将其数据输出到读取程序，不是吗？就我个人而言，当我第一次开始学习Java IO时，我发现这有点令人困惑。为了消除这种可能的混淆，我尝试在输入和输出上使用一些不同的名称，试图从概念上将它们与输入的来源和输出的去向联系起来。Java的IO包主要关注从源读取原始数据和将原始数据写入目标。最典型的数据来源和目的地如下：

* Files
* Pipes
* Network Connections
* In-memory Buffers (e.g.arrays)
* System.in,System.out,System.error
下图说明了程序从源读取数据并将其写入某个目标的原理：
![](Pasted%20image%2020221111160401.png)

## Streams

​	在Java IO中IO流是核心的概念。从概念上讲，流是无尽的数据流。你能从流中读取或者写入流。流连接到数据源或数据目标。Java IO中的流可以是基于字节的（读写字节），也可以是基于字符的（读和写字符）。

## The InputStream, OutputStream, Reader and Writer

​	需要从某个源读取数据的程序需要InputStream或Reader。需要将数据写入某个目标的程序需要OutputStream或Writer。下图也说明了这一点：

![](Pasted%20image%2020221114093807.png)
	InputStream或Reader链接到数据源。OutputStream或Writer链接到数据的目标。

## Java IO的功能和用途

​	Java IO包含InputStream、OutputStreet、Reader和Writer类的许多子类。原因是，所有这些子类都在处理各种不同的目的。这就是为什么有这么多不同的类。所述目的概述如下：

* File Access
-   Network Access
-   Internal Memory Buffer Access
-   Inter-Thread Communication (Pipes)
-   Buffering
-   Filtering
-   Parsing
-   Reading and Writing Text (Readers / Writers)
-   Reading and Writing Primitive Data (long, int etc.)
-   Reading and Writing Objects
		当阅读Java IO类时很容易了解这些目的。它们使人们更容易理解这些类的目标。