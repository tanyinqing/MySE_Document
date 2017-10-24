# Chapter 6 异常处理

> An exception is an event, which occurs during the execution of a program, that disrupts the normal flow of the program's instructions.

1. 异常的产生 会中断程序异常 产生了一个异常的实例
    - `java.lang.ArithmaticException  算数异常`
    - `java.lang.StringIndexOutOfBoundsException  字符串索引超出异常`
    - `java.lang.ArrayIndexOutOfBoundsException  数组索引越界异常`
    - `java.lang.NumberFormatException  数字格式异常`
    - `java.lang.NullPointerException  空指针异常`
        
2. 异常的处理后  catch块内的代码终止运行，但代码块外其他程序正常运行，  

 ```
 try {
     // 可能产生异常的语句块
 } catch (ExceptionType exceptionType) {
     // 异常的处理
 } finally {
     // 其他的处理
 }
    ```
    
    - `try` 后面必须有 `catch` 或 `finally`
    - `catch` 可以有多个
    - `finally` 最多只能有一个
    - `finally` 位于 `catch` 的后面
    - `try` 内一旦发生异常，`try` 内这条语句后的代码都不再执行，无论异常有没有被 `catch`
    - `finally` 语句块总是会被执行
    - 异常的处理方式
        - 输出异常信息 `e.printStackTrace();`
        - 退出程序 `System.exit(1)  主动退出 finally中的语句也退出`
        - 针对特定异常的更积极的处理方式

3. 异常的分类

    ```java
    java.lang.Object
        java.lang.Throwable 可以抛出的
            java.lang.Error  错误 无法处理
            java.lang.Exception  所有异常的父类
                java.lang.RuntimeException  运行时异常
                java.io.IOException
                *.*.*Exception
    ```

    - 非受检异常 `unchecked exception 可以通过编译`   另一个是多种因素造成的，不可避免的，程序员不可控的
        
        > RuntimeException类及其子类是非受检异常

    - 受检异常 `checked exception 不能通过编译，必须显示处理`  一个是不应该产生的，是程序员本身bug，
    
        > Exception类中除了RuntimeException之外的其他异常类及其子类
    
    - 非受检异常可以通过编译，可能在运行时产生
    - 受检异常不能通过编译，必须对其进行处理
        - 受检异常的处理方式
            1. 使用 `try` / `catch` 包围
            - 在方法中声明这个异常 `throws`

4. 显式抛出异常 `throw`

5. try-with-resources

    > since JDK 7

  ```java
  try (RandomAccessFile raf = new RandomAccessFile("path-to-file", "rw")){
      System.out.println();
  } catch (IOException e) {
      e.printStackTrace();
  }
  ```



