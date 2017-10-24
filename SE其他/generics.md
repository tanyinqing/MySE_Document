# Chapter 5 泛型 `Generic Types`

> since Java JDK 5

> generic 泛化的，通用的，一般的

这是它的应用实例
```
public class GenericTest<T> {
//    psvm 弹出主方法  sout 输出的快捷键  iter 增强for循环  ctrl+shift+上下箭头 上下移动行
   //运用泛型使方法变成通用的
    public String cancat(T x,T y){
        return String.valueOf(x)+String.valueOf(y);
    }

    public static void main(String[] args) {
//   generic 通用的 泛化的类型 general  一般的
        GenericTest genericTest=new GenericTest();
        System.out.println(genericTest.cancat(1,2));
        System.out.println(genericTest.cancat(1.0,"jjj"));
        System.out.println(genericTest.cancat(true,"jjj"));
}
}
```

1. 类型参数 `type parameters`
    ```
    class(interface) 类名（接口名）<类型参数列表 extends / super 类型 & 类型 & ...> {...}
    ```
    
    > 类型参数的命名 建议用下列参数

        E - Element (used extensively by the Java Collections Framework)
        K - Key  map接口中大量用
        V - Value
        N - Number
        T - Type 指代任意类型
        S,U,V etc. - 2nd, 3rd, 4th types
        
    > 有界类型
    
    ```
    //限制泛型类的类型只能是某些类的子类
    public class Calxulator<T extends Integer> {
    }
    
    public class Test<T extends Serializable>{
    //    psvm 弹出主方法  sout 输出的快捷键  iter 增强for循环  ctrl+shift+上下箭头 上下移动行
        public T test(T x){
            return x;
        }
    public static void main(String[] args) {
    // 定义的具体参数只能是定义泛型的子类
     Test<A> ta=new Test<>();
        System.out.println(new A());
    
    }
    }
    class A implements Serializable {
    
    
    }
    class B {
    
    }
    ```

    > PECS `Producer Extends, Consumer Super`
      
        extends
        super
   
2. 泛型的类
3. 泛型的接口的使用

```
public interface GenericInterface<T extends Serializable,E,S,U> {
//    psvm 弹出主方法  sout 输出的快捷键  iter 增强for循环  ctrl+shift+上下箭头 上下移动行

    T method(T t);
}
//实现一个泛型接口的话 类也要是泛型
/*
class GenericImpl<T> implements GenericInterface<T>{

    @Override
    public T method(T t) {
        return null;
    }
}*/
// 泛型的参数是有界类型  实现类要一致
class GenericImpl<T extends Serializable,E,S,U> implements GenericInterface<T,E,S,U>{

    @Override
    public T method(T t) {
        return null;
    }
}
```

## 泛型的作用
- 类型安全，附加了类型检查。避免强制类型转换时出现 `ClassCastException`
- 简化代码

```
 //泛型定义了集合中元素的类型  取得类型就安全了
        Vector<String> vector=new Vector();        
        vector.add("hi");
```
## 代码示例
- 泛型的使用

```
// 定义Apple类时使用了泛型声明
public class Apple<T>
{
    // 使用T类型形参定义实例变量
    private T info;
    public Apple(){}
    // 下面方法中使用T类型形参来定义构造器
    public Apple(T info)
    {
        this.info = info;
    }
    public void setInfo(T info)
    {
        this.info = info;
    }
    public T getInfo()
    {
        return this.info;
    }
    public static void main(String[] args)
    {
        // 由于传给T形参的是String，所以构造器参数只能是String
        Apple<String> a1 = new Apple<>("苹果");
        System.out.println(a1.getInfo());
        // 由于传给T形参的是Double，所以构造器参数只能是Double或double
        Apple<Double> a2 = new Apple<>(5.67);
        System.out.println(a2.getInfo());
    }
}
```
- 可变参数与泛型可以很好的共存

```
public class Test {
    public static void main(String[] args) {
        Test t = new Test();
        //t.list(1, 2, 3, 4, 5)  返回一个泛型的列表
        for (Integer i : t.list(1, 2, 3, 4, 5)) {
            System.out.printf(i + " ");
        }

    }
//可变参数与泛型可以很好的共存
    public <T> List<T> list(T... ts) {
        return Arrays.asList(ts);
    }
}

```
- 擦除的神秘之处

```
//        在泛型代码内部，无法获得任何有关泛型参数类型的信息
//        java 是使用擦除来实现的，这意味着当你使用泛型时，任何具体的类型信息都被擦除了。
        Class c1 = new ArrayList<String>().getClass();
        Class c2 = new ArrayList<Integer>().getClass();
        System.out.printf(c1.equals(c2) ? "true" : "false");

返回true
```