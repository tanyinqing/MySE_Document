<center><h1 style="magrin:0px;text-align:center;font-size:20px;">
Java - 大数据工程师培训
</h1></center>

### 17.10.20项目  泛型地址   https://github.com/tanyinqing/JavaSE_20170902

|类|说明|链接|
|---|---|---|
|GenericInterface|泛型接口|[地址](https://github.com/tanyinqing/JavaSE_20170902/blob/master/src/main/java/cn/edu/tsinghua/javase/generic/GenericInterface.java)|
|Test|泛型参数的有界类型|[地址](https://github.com/tanyinqing/JavaSE_20170902/blob/master/src/main/java/cn/edu/tsinghua/javase/generic/Test.java)|
|GenericTest|泛型的意义|[地址](https://github.com/tanyinqing/JavaSE_20170902/blob/master/src/main/java/cn/edu/tsinghua/javase/generic/GenericTest.java)|

### 17.10.23项目 `异常处理`
类|说明|链接|
|---|---|---|
|CheckedExceptionTest|受检异常|[地址](https://github.com/tanyinqing/JavaSE_20170902/blob/master/src/main/java/cn/edu/tsinghua/javase/exception/CheckedExceptionTest.java)|
|Test|异常|[地址](https://github.com/tanyinqing/JavaSE_20170902/blob/master/src/main/java/cn/edu/tsinghua/javase/exception/Test.java)|

### 17.10.24项目 `数据流的四个抽象类`
类|说明|链接|
|---|---|---|
|InputStreamTest|字节文件输入流|[地址](https://github.com/tanyinqing/JavaSE_20170902/blob/master/src/main/java/cn/edu/tsinghua/javase/io/InputStreamTest.java)|
|OutputStreamTest|字节文件输出流|[地址](https://github.com/tanyinqing/JavaSE_20170902/blob/master/src/main/java/cn/edu/tsinghua/javase/io/OutputStreamTest.java)|
|ReaderTest|读取文本类型的字符文件|[地址](https://github.com/tanyinqing/JavaSE_20170902/blob/master/src/main/java/cn/edu/tsinghua/javase/io/ReaderTest.java)|
|WriterTest|写一个文本类型的字符文件|[地址](https://github.com/tanyinqing/JavaSE_20170902/blob/master/src/main/java/cn/edu/tsinghua/javase/io/WriterTest.java)|


- 学习文件英文源码 鼠标放在方法或类上 快捷键 ctrl+q
```
 // 将读取的数据写入临时文件
                tmpOut.write(bbuf , 0 , hasRead);
                
java.io.FileOutputStream
public void write(@NotNull byte[] b,  参数不能为空
                  int off,
                  int len)
          throws java.io.IOException
External annotations available: 
@org.jetbrains.annotations.NotNull
Writes len bytes from the specified byte array starting at offset off to this file output stream.
Overrides:  从指定的字节数组中从起始偏移量写入该文件输出流。          
write in class OutputStream
Parameters: 参数
b - the data.
off - the start offset in the data.
len - the number of bytes to write.
Throws:
java.io.IOException - if an I/O error occurs.
```
  