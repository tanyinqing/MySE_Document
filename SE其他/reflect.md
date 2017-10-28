# 补2. 反射 `Reflect`

> 比较高级的特性 Reflection: This is a relatively advanced feature and should be used only by developers who have a strong grasp of the fundamentals of the language.

1. java.lang.reflect 下面是这个包下全部的类
    - `AccessibleObject` 
    - `Array`
    - `Constructor 构造器` 
    - `Field 域` 
    - `Method  方法`
    - `Modifier  修饰符` 
    - `Proxy`
    - `ReflectPermission`

- 通过反射获取ArrayList这个类的一个隐藏的域

```
public static void main(String[] args) {
    List<String> strings=new ArrayList<>();
    for (int i = 0; i < 10; i++) {
        strings.add("hi");
    }

    strings.add("hello");
    System.out.println(strings.size());
    try {
        //获得所在类的类对象 下面三种方法
        // 这个变量 源文件中是默认的，不允许外包中访问
        Class mclass=Class.forName("java.util.ArrayList");
        Field field=mclass.getDeclaredField("elementData");
//        Field field=ArrayList.class.getDeclaredField("elementData");
//        Field field=strings.getClass().getDeclaredField("elementData");
        field.setAccessible(true);//设置可以访问的
        int capacity=((Object[])field.get(strings)).length;
        System.out.println(capacity);
    } catch (NoSuchFieldException e) {
        e.printStackTrace();
    } catch (IllegalAccessException e) {
        e.printStackTrace();
    } catch (ClassNotFoundException e) {
        e.printStackTrace();
    }
}
```
2. Java 类的加载机制
    - 加载 `loading`
        1. 加载器分类
            - 启动类加载器 `bootstrap class loader` 
            - 自定义加载器 `user-defined class loader`
            - 系统类加载器 `system class loader`
        2. 过程
            - 通过一个类的全限定名来获取其定义的二进制字节流
            - 将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构
            - 在 `Java` 堆中生成一个代表这个类的 `java.lang.Class` 对象  这个是重点
        3. 结果：`byte code` ---> `java.lang.Class` 对象
            
    - 链接 `linking`
        - 验证 `verification`
        - 准备 `preparapent`
        - 解析 `resuolutation`
        
    - 初始化 `initialization`

3. java.lang.Class  获得类对象的方法
    - ClassName.class;
    - instance.getClass();
    - Class.forName(String className);
    
    ```
    //获得所在类的类对象 下面三种方法
            Class mclass=Class.forName("java.util.ArrayList");
            Field field=mclass.getDeclaredField("elementData");
    //        Field field=ArrayList.class.getDeclaredField("elementData");
    //        Field field=strings.getClass().getDeclaredField("elementData");
    ```
    
4. A demo `Human` class

- 动物 父类

    ```java
    // super class Animals
    class Animals {
        public int age; // It's public
        private double weight;
    
        public Animals() {
        }
    
        public Animals(int age, double weight) {
            this.age = age;
            this.weight = weight;
        }
    
        public int sleep(int hours) {
            return hours;
        }
    
        public void eat(String food) {
            System.out.println("eating " + food);
        }
        
        // This's a private method!
        private void killHuman() {
            System.out.println("killed a poor guy...");
        }
        
        // getters and setters
    }
    ```
- 人类

    ```java
    // sub class Human
    public final class Human extends Animals {
        public String name; // It's public!
        private boolean married;
    
        Human() { // It's package-private!
        }
    
        public Human(int age, double weight, String name, boolean married) {
            super(age, weight);
            this.name = name;
            this.married = married;
        }
    
        @Override
        public void eat(String food) {
            System.out.println(name + " is now eating " + food);
        }
    
        public void study(String course) {
            System.out.println(name + " is now studying " + course);
        }
    
        // This's a private method!
        private void killAnimals(String animal) {
            System.out.println(name + " is now killing " + animal);
        }
        
        // getters and setters
    }
    ```

5. Fields 获取变量  可以在运行时通过反射获得类的任何内容，包括私有的，破坏了封装性
    - `getFields() 所有公开的`

        > All the public fields up the entire class hierarchy.

    - `getDelcaredFields() 共有的私有的都可以`

        > All the fields, regardless of their accessibility but only for the current class 

    ```java
    class HumanTest {
        public static void main(String[] args) {
            Human human = new Human();
            Field[] fields = human.getClass().getFields();
            System.out.println("--- getFields() 返回所有公有的变量包括继承的父类---");
            for (Field field : fields) {
                System.out.println(field.getName());
            }
            Field[] declaredFields = human.getClass().getDeclaredFields();
            System.out.println("--- getDeclaredFields()  返回所有的变量  但仅是当前类---");
            for (Field declaredField : declaredFields) {
                System.out.println(declaredField.getName());
            }
        }
    }
    
    /*
    --- getFields() ---
    name
    age
    --- getDeclaredFields() ---
    name
    married
     */
    ```
- 使用场景

    ```
    // 通过反射获取 ArrayList 的容量
    List<Integer> list = new ArrayList<>();
    Field array = ArrayList.class.getDeclaredField("elementData");
    array.setAccessible(true);
    System.out.println("list capacity: " + ((Object[]) array.get(list)).length); // 10
    ```

6. Constructors 构造器

    - getConstructors

        > only public constructors

    - getDeclaredConstructors

        >  all the constructors

    ```java
    class HumanTest {
        public static void main(String[] args) {
            Human human = new Human();
            Constructor[] constructors = human.getClass().getConstructors();
            System.out.println("--- getConstructors 公共的构造器---");
            for (Constructor constructor : constructors) {
                System.out.println(constructor.getName());
   //          获得构造器中的参数
                for (Parameter parameter : constructor.getParameters()) {
                    System.out.println("\t" + parameter);
                }
            }
    
            Constructor[] declaredConstructors = human.getClass().getDeclaredConstructors();
            System.out.println("--- getDeclaredConstructors 所有的构造器---");
            for (Constructor declaredConstructor : declaredConstructors) {
                System.out.println(declaredConstructor.getName());
                for (Parameter parameter : declaredConstructor.getParameters()) {
                    System.out.println("\t" + parameter);
                }
            }
        }
    }
    
    /*
    --- getConstructors ---
    Human
        int arg0
        double arg1
        java.lang.String arg2
        boolean arg3
    --- getDeclaredConstructors ---
    Human  这个是无参的构造方法  修饰符默认的 不允许外包访问
    Human
        int arg0
        double arg1
        java.lang.String arg2
        boolean arg3
     */
    ```
- 使用场景
    
    ```
    // constructor - object  运用获得的构造器进行实例化
    Human human = null;
    try {
        human = (Human) constructor.newInstance(20, 60, "Tom", false);
        System.out.println(human.getAge());
    } catch (InstantiationException | IllegalAccessException | InvocationTargetException e) {
        e.printStackTrace();
    }
 
    /*
    20
   */
    ```

7. Methods  获得所有的方法

    - getMethods

        > All the public methods up the entire class hierarchy.

    - `getDelcaredMethods()`

        > All the methods, regardless of their accessibility but only for the current class 

    ```java
    class HumanTest {
        public static void main(String[] args) {
            Human human = new Human();
            Method[] methods = human.getClass().getMethods();
            System.out.println("--- getMethods 公有的方法包括父类包括父类的父类例如object---");
            for (Method method : methods) {
                System.out.println(method);
            }
            Method[] declaredMethods = human.getClass().getDeclaredMethods();
            System.out.println("--- getDeclaredMethods 所有的方法 但仅限于本类---");
            for (Method declaredMethod : declaredMethods) {
                System.out.println(declaredMethod);
            }
        }
    }
    
    /*
    --- getMethods ---
    public int java1702.javase.regex.Human.sleep(int)
    public void java1702.javase.regex.Human.study(java.lang.String)
    public void java1702.javase.regex.Human.eat(java.lang.String)
    public final void java.lang.Object.wait(long,int) throws java.lang.InterruptedException
    public final native void java.lang.Object.wait(long) throws java.lang.InterruptedException
    public final void java.lang.Object.wait() throws java.lang.InterruptedException
    public boolean java.lang.Object.equals(java.lang.Object)
    public java.lang.String java.lang.Object.toString()
    public native int java.lang.Object.hashCode()
    public final native java.lang.Class java.lang.Object.getClass()
    public final native void java.lang.Object.notify()
    public final native void java.lang.Object.notifyAll()
    --- getDeclaredMethods ---
    public int java1702.javase.regex.Human.sleep(int)
    public void java1702.javase.regex.Human.study(java.lang.String)
    private void java1702.javase.regex.Human.killAnimals(java.lang.String)
    public void java1702.javase.regex.Human.eat(java.lang.String)
     */
    ```
- 使用场景 调用反射获得的方法

```
   Method study = Human.class.getMethod("study", String.class, int.class);
        System.out.println(Modifier.toString(study.getModifiers()));

        Human human = new Human();
        human.setName("Jerry");
//调用反射得到的方法
        study.invoke(human,"Java SE", 2); // invoke 调用\ [ɪn'vəʊk] call
```

8. Modifiers 进行限定修饰符

    ```java
    class HumanTest {
        public static void main(String[] args) throws NoSuchFieldException {
            Human human = new Human();
            System.out.println(Modifier.toString(human.getClass().getModifiers()));
            Field field = human.getClass().getField("name");
            System.out.println(Modifier.toString(field.getModifiers()));
       //还有就是方法的修饰符
    //用反射的方法使用
     }
    }
    
    /*
    public final  这个是类的限定修饰符
    public   这个是name这个类的变量的限定修饰符
     */
    ```