# Java IO：流

​	Java IO流是可以读取或写入的数据流。如Java IO概述中所述，流通常连接到数据源或数据目的地，如文件或网络连接。

​	流和数组一样，没有读取或写入数据的索引的概念。也不能像在数组或使用RandomAccessFile的文件中那样，在流中来回移动。流只是连续的数据流。

​	一些流实现（如PushbackInputStream）允许您将数据推回到流中，稍后重新阅读。但您只能推回有限的数据量，不能像使用数组那样随意遍历数据。只能按顺序访问数据。

​	Java IO流通常基于字节或字符。基于字节的流通常被称为“流”，如InputStream或OutputStreet。这些流一次读取和写入一个原始字节，除了DataInputStream和DataOutputStreet，它们还可以读取和写入int、long、float和double值。基于字符的流通常称为“Reader”或“Writer”。基于字符的流可以读取/写入字符（如Latin1或UNICODE字符）。有关基于字符的输入和输出的更多信息，请参阅文本Java Readers and Writers。

## InputStream

​	java.io.InputStream类是所有Java IO输入流的基类。如果您正在编写一个需要从流读取输入的组件，请尝试使我们的组件依赖于InputStream，而不是它的任何子类（例如FileInputStriam）。这样做可以使代码能够处理所有类型的输入流，而不仅仅是具体的子类。

​	然而，仅依赖InputStream并不总是可能的。如果您需要能够将数据推回到流中，则必须依赖PushbackInputStream-这意味着您的流变量将是这种类型。否则，您的代码将无法对PushbackInputStream调用unread（）方法。

​	通常通过调用read（）方法从InputStream读取数据。read（）方法返回一个int，其中包含字节读取的字节值。如果没有更多要读取的数据，read（）方法通常返回-1；

```java
InputStream input = new FileInputStream("C:\\data\\input-file.txt");
int data = input.read();
while(data != -1){
    data = input.read();
}
```

## OutputStream

​	java.io.OutputStream类是所有Java IO输出流的基类。如果您正在编写需要将输出写入流的组件，请尝试确保该组件依赖于OutputStream，而不是其子类之一。

```java
OutputStream output = new FileOutputStream("C:\\data\\output-file.txt");
output.write("Hello World".getBytes());
output.close();
```

## 组合流

​	可以将流组合成链，以实现更高级的输入和输出操作。例如，从文件中一次读取一个字节是很慢的。从磁盘中读取更大的数据块，然后逐个字节地迭代该数据块会更快。要实现缓冲，可以将InputStream包装在BufferedInputStream中。

```java
InputStream input = new BufferedInputStream(new FileInputStream("C:\\data\\input-file.txt"));
```

​	缓冲也可以应用于OutputStream，从而将写入磁盘（或底层流）的数据分成更大的块。这也提供了更快的输出。这是通过BufferedOutputStream完成的。缓冲只是通过组合流可以实现的效果之一。你还可以将InputStream包装在PushbackStream中。这样，你可以将数据推回到流中，以便稍后重新读取。这在解析过程中有时很方便。或者，你可以使用SequenceInputStream将两个输入流合并为一个。通过将输入和输出流组合成链，还可以实现其他几种效果。你甚至可以编写自己的流类来包装Java附带的标准流类。这样，你可以创建自己的效果或过滤器。

