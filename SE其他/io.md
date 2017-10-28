# Chapter 7 Stream & File  数据流 有向流动的数据  
- 存储路径有相对路径和绝对路径 
    - 相对路径，只有名称，路径是相对于当前路径而定的
    - 绝对路径，是标明了在跟目录的某个位置

1. `InputStream 输入流` / `OutputStream 输出流` / `Reader` / `Writer`  读取文件是一个字节一个字节读取的

   > 都是抽象类，不能实例化，只能作为父类使用。用已知子类实例化。注意需要 `close() 释放系统资源`
   
   > 输入输出是对程序而言的 
   - D:/tan.txt  wondows路径
   - src/main/java/cn/edu/tsinghua/javase/ceshi/test.java  相对当前文件目录的路径

   * `InputStream`  子类例如FileInputStream文件输入流 实例化
     * 基于 字节 的输入流  逐个输出一个一个的字节 read一次读一个字节
   * `OutputStream`
     * 基于 字节 的输出流
   * `Reader`   FileReader是Reader子类 从文件中读出数据
     * 基于 字符 的输入流  适合文本文件 2到3个字节
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
- 实例代码 
     
- 文件先写后读

```
public static void main(String[] args) {
        try (RandomAccessFile randomAccessFile = new RandomAccessFile("test", "rw");
        ) {//指针逐个移动  写数据
            for (int i = 0; i < 10; i++) {
                randomAccessFile.writeDouble(i*0.5);
            }//一个Double占8个字节
            randomAccessFile.seek(8);//指针移动到0字节的位置
            System.out.println(randomAccessFile.readDouble());
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
```
- 从文件的制定位置读取内容
```
public static void main(String[] args)
    {
        try(
                RandomAccessFile raf =  new RandomAccessFile(
                        "src/main/java/cn/edu/tsinghua/javase/yuxi/RandomAccessFileTest.java" , "r"))// 表明文件只能读取
        {
            // 获取RandomAccessFile对象文件指针的位置，初始位置是0
            System.out.println("RandomAccessFile的文件指针的初始位置："
                    + raf.getFilePointer());
            // 移动raf的文件记录指针的位置  从文件的第300个字节处开始读取文件
            raf.seek(300);
            byte[] bbuf = new byte[1024];
            // 用于保存实际读取的字节数
            int hasRead = 0;
            // 使用循环来重复“取水”过程
            while ((hasRead = raf.read(bbuf)) > 0 )
            {
                // 取出“竹筒”中水滴（字节），将字节数组转换成字符串输入！
                System.out.print(new String(bbuf , 0 , hasRead ));
            }
        }
        catch (IOException ex)
        {
            ex.printStackTrace();
        }
    }
```
- 在文件的结尾追加内容

```
 public static void main(String[] args)
    {
        try(
                //以读、写方式打开一个RandomAccessFile对象
                RandomAccessFile raf = new RandomAccessFile("out.txt" , "rw"))
        {
            //将记录指针移动到out.txt文件的最后
            raf.seek(raf.length());
            raf.write("追加的内容！\r\n".getBytes());
        }
        catch (IOException ex)
        {
            ex.printStackTrace();
        }
    }
```
- 向指定文件指定位置插入内容的功能 建立临时文件，先把文件读到临时文件，在添加内容，在把临时文件写入文件

```
文件名 文件插入位置 插入的内容
  public static void insert(String fileName , long pos
            , String insertContent) throws IOException
    {
        //建立一个临时文件 该文件将在JVM退出时删除
        File tmp = File.createTempFile("tmp" , null);
        tmp.deleteOnExit();
        try(
                RandomAccessFile raf = new RandomAccessFile(fileName , "rw");
                // 使用临时文件来保存插入点后的数据
                FileOutputStream tmpOut = new FileOutputStream(tmp);
                FileInputStream tmpIn = new FileInputStream(tmp))
        {
            raf.seek(pos);
            // ------下面代码将插入点后的内容读入临时文件中保存------
            byte[] bbuf = new byte[64];
            // 用于保存实际读取的字节数
            int hasRead = 0;
            // 使用循环方式读取插入点后的数据
            while ((hasRead = raf.read(bbuf)) > 0 )
            {
                // 将读取的数据写入临时文件
                tmpOut.write(bbuf , 0 , hasRead);
            }
            // ----------下面代码插入内容----------
            // 把文件记录指针重新定位到pos位置
            raf.seek(pos);
            // 追加需要插入的内容
            raf.write(insertContent.getBytes());
            // 追加临时文件中的内容
            while ((hasRead = tmpIn.read(bbuf)) > 0 )
            {
                raf.write(bbuf , 0 , hasRead);
            }
        }
    }
    public static void main(String[] args)
            throws IOException
    {
        insert("InsertContent.java" , 45 , "插入的内容\r\n");
    }
```

3. `BufferedInputStream` / `BufferedOutputStream` / `BufferedReader` / `BufferedWriter`  缓冲流也叫包装流，读取效率更高

   > 提高输入输出效率 加入缓冲的功能，主要用到这4个类

   * `bufferedReader.readLine() 一次读取一行`
   * BufferedInputStream(InputStream in)   创建一个 BufferedInputStream 并保存其参数，即输入流 in，以便将来使用。所以使用抽象方法的实现类做为参数；
   
```
 BufferedInputStream inputStream = new BufferedInputStream(new FileInputStream("/Users/mingfei/Desktop/1025_JavaSE-RandomAccessFile.mov"));
                BufferedOutputStream outputStream = new BufferedOutputStream(new FileOutputStream("test.mov"))
```
- 使用缓冲流，一边读文件，一边写文件

```
 public static void main(String[] args) {
        // 缓冲流比较快
        try (
//                InputStream inputStream = new FileInputStream("/Users/mingfei/Desktop/1025_JavaSE-RandomAccessFile.mov");
//                OutputStream outputStream = new FileOutputStream("test.mov")
                BufferedInputStream inputStream = new BufferedInputStream(new FileInputStream("/Users/mingfei/Desktop/1025_JavaSE-RandomAccessFile.mov"));
                BufferedOutputStream outputStream = new BufferedOutputStream(new FileOutputStream("test.mov"))
        ) {
            int i;
            while ((i = inputStream.read()) != -1) {
                outputStream.write(i);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```
- 使用缓冲流下载一个图片

```
public class DownloadImage {
    private static final String IMAGE_URL = "http://img.jandan.net/news/2017/09/cf114fae2a31b13bac5a13c5bce745df.jpg";

    public static void main(String[] args) {
//        java.net.URL
        try {
            URL url = new URL(IMAGE_URL);
//            System.out.println(url.getFile());
            try (
                    BufferedInputStream inputStream = new BufferedInputStream(url.openStream());
                    BufferedOutputStream outputStream = new BufferedOutputStream(new FileOutputStream("test.jpg"))
            ) {
//                int i;
//                while ((i = inputStream.read()) != -1) {
//                    outputStream.write(i);
//                }
                // 8bit = 1byte  1个字节等于8个位
                int i = inputStream.read();//这个向当于每次读出一个字节 也就是8个0或1的组合
                while (i != -1) {
                    outputStream.write(i); //字节逐个输入
                    i = inputStream.read();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }
    }
}
```
- 使用BufferedReader这个缓冲字节流，一次读取一行，要比字符流快

```
  public static void main(String[] args) {
        try (
                BufferedReader bufferedReader = new BufferedReader(new FileReader("src/main/java/cn/edu/tsinghua/javase/ceshi/ReadLineTest.java"));
        ) {
            String line;
            while ((line = bufferedReader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```
4. `File`

   * `File` 指代文件 `file` 或目录 `directory`
   * `File` 不处理文件内容，只处理文件或目录的周边信息
   * `File` 常用方法
     * `canRead  是否可读 windows下都可读`
     * `canWrite  是否可写`
     * `createNewFile 创建一个文件`
     * `delete 删除文件`
     * `deleteOnExit  程序执行完后把文件删除`
     * `getAbsoluteFile 获取相对路径，返回一个文件`
     * `getAbsolutePath  获取相对路径，返回一个文件的字符串路径`
     * `getName 文件名`
     * `getParent 父级 需指定绝对目录 否则可能为null `
     * `getParentFile 返回一个文件`
     * `getPath`
     * `getTotalSpace 返回分区空间的总大小`
     * `getUsableSpace 可以空间大小`
     * `isAbsolute 是否是绝对路径`
     * `isDirectory`
     * `isFile`
     * `isHidden  是否是隐藏的`
     * `lastModified 最后一次修改时间 返回时间毫秒值`
     * `length 文件的字节数`
     * `list 返回目录`
     * `listFiles 返回文件的数组`
     * `listRoots 根目录`
     * `mkdir `
     * `mkdirs   File file = new File("a/b/c");  多重目录` 
     * `renameTo 改名`
     * `setLastModified  设置最后一次修改时间`
     * `setReadable 设置可读 就不能写入了` 
     * `setReadOnly`
     * `setWritable`

- FileTest的实例代码

```
指定文件是绝对路径
File file = new File("/Users/mingfei/IdeaProjects/JavaSE_20170902/data");
指定文件是相对路径
  File file = new File("Test.jpg");
  
  
//        File file = new File(".idea");

//        file.createNewFile();
//
//        System.out.println(file.isFile());
//        System.out.println(file.isDirectory());
//
//        System.out.println(file.canRead());
//        System.out.println(file.canWrite());

//        file.delete();

//        file.deleteOnExit();

//        Thread.sleep(1000 * 10);

//        System.out.println(file.getAbsoluteFile().toString());
//        System.out.println(file.getAbsolutePath());
//
//        System.out.println(file.getName());
//        System.out.println(file.getParent());
//        System.out.println(file.getParentFile());
//
//        System.out.println(file.getTotalSpace());
//        System.out.println(file.getUsableSpace());
//
//
//        System.out.println(file.isAbsolute());
//        System.out.println(file.isHidden());
//
//        System.out.println(new Date(file.lastModified()));
//
//        System.out.println(file.length());
//
//        for (File f : file.listFiles()) {
//            System.out.println(f);
//        }
//
//        for (File file1 : file.listRoots()) {
//            System.out.println(file1);
//        }

    //////////


    File file = new File("test.jpg");
//        file.delete();
//        System.out.println(file.mkdir()); // make directory
//        System.out.println(file.mkdirs());

//        file.setLastModified(-100000000000L);

    System.out.println(new Date(file.lastModified()));
```
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
- 从一个网站下载多张图片  

```
public class Homework {
//    psvm 弹出主方法  sout 输出的快捷键  iter 增强for循环  ctrl+shift+上下箭头 上下移动行
private static final String HTML_URL = "http://jandan.net/page/";
public static void main(String[] args) throws MalformedURLException {
//        URL.openStream()
//        BufferedReader.readLine()

    for (int i = 1; i < 100; i++) {

        URL url = new URL(HTML_URL + i);

        try (BufferedReader reader = new BufferedReader(new InputStreamReader(url.openStream()))) { // InputStreamReader: inputStream => Reader
            String line;
            while ((line = reader.readLine()) != null) {
            // 打开文件的源码  从源码中找地址
                if (line.contains("<div class=\"thumbs_b\">")) {
                    String imageUrl = "http:" + line.substring(line.indexOf("//img"), line.indexOf("!custom"));
                    DownloadImage.download(imageUrl);
                    System.out.println(imageUrl);
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}
}
```
- 从一个网站下载多张图片  调用的方法 DownloadImage.download(imageUrl);

```
private static int counter;
    public static void download(String imageUrl){
        try {
            URL url = new URL(imageUrl);
//            System.out.println(url.getFile());
            try (
                    BufferedInputStream inputStream = new BufferedInputStream(url.openStream());
                    BufferedOutputStream outputStream = new BufferedOutputStream(new FileOutputStream("D:/tan/tan"+ (++counter) + ".jpg"))
            ) {
//                int i;
//                while ((i = inputStream.read()) != -1) {
//                    outputStream.write(i);
//                }
                // 8bit = 1byte  1个字节等于8个位
                int i = inputStream.read();//这个向当于每次读出一个字节 也就是8个0或1的组合
                while (i != -1) {
                    outputStream.write(i); //字节逐个输入
                    i = inputStream.read();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }
    }
```