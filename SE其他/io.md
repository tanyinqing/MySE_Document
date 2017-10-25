# Chapter 7 Stream & File  数据流 有向流动的数据

1. `InputStream 输入流` / `OutputStream 输出流` / `Reader` / `Writer`

   > 都是抽象类，不能实例化，只能作为父类使用。用已知子类实例化。注意需要 `close() 释放系统资源`
   
   > 输入输出是对程序而言的 
   - D:/tan.txt  wondows路径
   - src/main/java/cn/edu/tsinghua/javase/ceshi/test.java  相对当前文件目录的路径

   * `InputStream`  子类例如FileInputStream文件输入流 实例化
     * 基于 字节 的输入流  逐个输出一个一个的字节 read一次读一个字节
   * `OutputStream`
     * 基于 字节 的输出流
   * `Reader`   FileReader是Reader子类 从文件中读出数据
     * 基于 字符 的输入流  适合文本文件
   * `Writer`    writer.flush(); 把缓存的内容写到文件
     * 基于 字符 的输出流
   * 从文件输入到程序里是输入流，参考是对程序本身而言
   * 以上4个类是抽象类，不能实例化，所以用它们的已知子类进行实例化。实例化的子类有如下几个类，分别是
   FileInputStream，FileOutputStream，ReaderTest，FileWriter。分别是针对文件的读写操作。

2. `RandomAccessFile`

   > 基本取代 `DataInputStream` 和 `DataOutputStream`

   ```java
    public class DataInputStream
    extends FilterInputStream
    implements DataInput

    public class DataOutputStream
    extends FilterOutputStream
    implements DataOutput

    public class RandomAccessFile
    extends Object
    implements DataOutput, DataInput, Closeable
   ```

3. `BufferedInputStream` / `BufferedOutputStream` / `BufferedReader` / `BufferedWriter`  缓冲流

   > 提高输入输出效率

   * `bufferedReader.readLine()`

4. `File`

   * `File` 指代文件 `file` 或目录 `directory`
   * `File` 不处理文件内容，只处理文件或目录的周边信息
   * `File` 常用方法
     * `canRead`
     * `canWrite`
     * `createNewFile`
     * `delete`
     * `deleteOnExit`
     * `getAbsoluteFile`
     * `getAbsolutePath`
     * `getName`
     * `getParent`
     * `getParentFile`
     * `getPath`
     * `getTotalSpace`
     * `getUsableSpace`
     * `isAbsolute`
     * `isDirectory`
     * `isFile`
     * `isHidden`
     * `lastModified`
     * `length`
     * `list`
     * `listFiles`
     * `listRoots`
     * `mkdir`
     * `mkdirs`
     * `renameTo`
     * `setLastModified`
     * `setReadable`
     * `setReadOnly`
     * `setWritable`

- File类的代码

```

import java.io.*;

public class FileTest
{
	public static void main(String[] args)
		throws IOException
	{
		// 以当前路径来创建一个File对象
		File file = new File(".");
		// 直接获取文件名，输出一点
		System.out.println(file.getName());
		// 获取相对路径的父路径可能出错，下面代码输出null
		System.out.println(file.getParent());
		// 获取绝对路径  D:\TanYinQingJavaEEStudy\GeRenXiangMu\JavaSE_20170902\.
		System.out.println(file.getAbsoluteFile());
		// 获取上一级路径
		System.out.println(file.getAbsoluteFile().getParent());
		// 在当前路径下创建一个临时文件
		File tmpFile = File.createTempFile("aaa", ".txt", file);
		// 指定当JVM退出时删除该文件
		tmpFile.deleteOnExit();
		// 以系统当前时间作为新文件名来创建新文件
		File newFile = new File(System.currentTimeMillis() + "");
		System.out.println("newFile对象是否存在：" + newFile.exists());
		// 以指定newFile对象来创建一个文件
		newFile.createNewFile();
		// 以newFile对象来创建一个目录，因为newFile已经存在，
		// 所以下面方法返回false，即无法创建该目录
		newFile.mkdir();
		// 使用list()方法来列出当前路径下的所有文件和路径
		String[] fileList = file.list();
		System.out.println("====当前路径下所有文件和路径如下====");
		for (String fileName : fileList)
		{
			System.out.println(fileName);
		}
		// listRoots()静态方法列出所有的磁盘根路径。
		File[] roots = File.listRoots();
		System.out.println("====系统所有根路径如下====");
		for (File root : roots)
		{
			System.out.println(root);
		}
	}
}

```
- 字符串输入流

```
public static void main(String[] args)
	{
		try(
			FileWriter fw = new FileWriter("poem.txt"))
		{
			fw.write("锦瑟 - 李商隐\r\n");
			fw.write("锦瑟无端五十弦，一弦一柱思华年。\r\n");
			fw.write("庄生晓梦迷蝴蝶，望帝春心托杜鹃。\r\n");
			fw.write("沧海月明珠有泪，蓝田日暖玉生烟。\r\n");
			fw.write("此情可待成追忆，只是当时已惘然。\r\n");
		}
		catch (IOException ioe)
		{
			ioe.printStackTrace();
		}
	}
```