		Java IO是Java附带的API用于读取或写入数据（输入和输出）。大多数应用程序需要处理一些输入并根据输入产生输出。例如：从文件或者网络读取数据，并通过网络写入文件或者写回响应。
		Java IO的API位于Java IO的包中（java.io）。如果你看看在java.io中的Java IO类大量选择会让人困惑。这些类的作用是什么？对于给定的任务你应该选择哪一个？如何创建自己的类的插件？
		这个教程的目的是试图给你一个这些类是怎么分组的概述和它们背后的目的，所以你不用怀疑是否选择了一个正确的类，或者是否已经存在了适合您的类。
# 跨越Java版本的Java IO 
		Java IO的API自从它第一次被创建后的许多Java版本中保持了相当的稳定。可是还是有一些小的改动，比如如何使用try with resources构造最好地关闭InputStream或OutputStream。本教程已经在很多地方进行了更新以反映这些发生的更改。
# Java IO概述
		开始学习Java IO的一个好的地方是Java IO的概述教程。本教程给你快速概述了Java IO API中的中心概念和其中的中心类。
# Java IO包的范围
		java.io包并不解决所有的输入和输出。例如：Java IO包不包括GUI和网页的输入和输出。这些类型的输入在其他地方有介绍，比如Swing工程的JFC类和Java EE的Servlet和HTTP包。
		Java IO包主要关注文件、网络流、内部内存缓冲区的输入和输出。但是Java IO包不包括网络通讯必须的打开网络套接字的类。为此你需要使用Java Networking API。一旦你打开了一个套接字就可以通过Java IO的InputStream和OutputStream类对其进行数据读写。
# Java NIO - 可替换的IO API
		Java包括另一种被称为Java NIO的IO API。它包括的类功能与Java IO和Java Networking大致相同，但是Java NIO可以在不阻塞模式下工作。在某些情况下，非阻塞IO可以大大提高阻塞IO的性能。
# 更多的Java IO工具和提示
		名为Java How To’s and Utilities的教程还包含一些Java IO实用程序，例如替换流中的字符串、使用缓冲区迭代流等。
# Java IO类概述表

![[Java IO.svg]]
