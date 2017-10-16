8. `static`
    - 静态
    - 可以修饰域和方法
    - 静态的成员隶属于`类对象` 也就可是可以直接用类名来引用
    - 静态方法中只能直接引用静态成员
    - 静态方法中不能使用 `this` 和 `super`
    - 方法中不能定义静态变量
    - 静态导入（JDK 1.5+）

      ```java
      import static java.lang.System.out
      ```
      
    - 静态块 `static block`
    
    > 静态块在类加载时自动执行一次, 之后不再执行
    
      ```java
      static {
        // ...
      }
      ```