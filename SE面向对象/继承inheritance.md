2. 继承 `inheritance`
    - `extends` 扩展
    - `子类`(`sub class`) `extends`(`继承`) `父类`(`super class`)
        - 子类拥有父类的域和方法
        
        > 注意父类成员的访问限定修饰符
            1. 父类的 `default` 成员，只有同包子类可继承
            2. 父类的 `private` 成员，不能继承

        - 子类可以有自己的域和方法
    - `super` 指代父类
    - 父类有无参构造方法
      - 子类可以隐式调用父类的无参构造方法
    - 父类没有无参构造方法
      - 子类必须显式调用父类的有参构造方法
      - 子类显式调用父类构造方法时，必须在其构造方法的第一行
      - 类加载顺序
      
      > 父类静态代码块内容 - 子类静态代码块内容 - 父类构造器块 - 父类构造器 - 子类构造器块 - 子类构造器

      ```java
      //这个是父类
      public class Parent {

          {
              System.out.println("parent constructor block");
          }
        //父类静态代码块内容
          static {
              System.out.println("parent static block");
          }

          public Parent() {
              System.out.println("parent constructor");
          }
      }


      class Child extends Parent {

          {
              System.out.println("child constructor block");
          }

          static {
              System.out.println("child static block");
          }

          public Child() {
              System.out.println("child constructor");
          }
      }

      class Test {
          public static void main(String[] args) {
              new Child();
          }
      }
      
      /*
      parent static block
      child static block
      parent constructor block
      parent constructor
      child constructor block
      child constructor
      */
      ```
    - Java 语言里，类是单继承的（接口可以多实现）
    - `instanceof` 判断对象是否是某个类的实例