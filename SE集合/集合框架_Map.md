### Map

> `Key - Value` 对结构 哈希表 键值对
  
- `Hashtable`
  
  > 无序

  > `non-null` and key `non-null` value  都不能为空 键唯一
  
  ![Hashtable](../image/javase/diagram/Hashtable.png)
  
- `HashMap 用的比较多`

  > 无序
  
  > `null` key and `null` value 键和值可以为空
  
  ![HashMap](../image/javase/diagram/HashMap.png)
  
- `LinkedHashMap`

  > 使用 `Hashtable` 实现

  > 按元素添加顺序排序
  
  > `null` key and `null` value  
  
  ![LinkedHashMap](../image/javase/diagram/LinkedHashMap.png)
  
- `TreeMap`

  > 使用 `红-黑 树` 存储元素

  > 按元素键的值排序

  > `non-null` key and `null` value
  
  ![TreeMap](../image/javase/diagram/TreeMap.png)
  
- ~~`WeakHashMap用的比较少`~~
  
  ![WeakHashMap](../image/javase/diagram/WeakHashMap.png)
  
- ~~`IdentityHashMap用的比较少`~~
  
  ![IdentityHashMap](../image/javase/diagram/IdentityHashMap.png)

### Iterator / ListIterator  提供循环服务

- `Iterator  迭代器 比较常用`
- `ListIterator`

  ![ListIterator](../image/javase/diagram/ListIterator.png)

#### Iterator Vs ListIetrator

- Iterator 可用于遍历 List 和 Set  因为它们实现了接口

  > ListIterator 只能遍历 List

- Iterator 只能向后遍历

  > ListIterator 能向前或向后遍历

- 使用 Iterator 不能获得 index

  > 使用 ListIterator 可以在任何时刻取得 index，使用 `nextIndex` 和 `previousIndex` 方法

- 使用 Iterator 遍历时不能添加元素，会抛出 `ConcurrentModificationException` 异常

  > 使用 ListIterator 遍历时可以使用 `add` 方法添加元素

- 使用 Iterator 时不能替换元素

  > 使用 ListIterator 可以使用 `set` 方法替换元素


- Iterator 的常用方法
  - hasNext
  - next
  - remove

```
这是它的使用方法  
 ArrayList<Integer>list=new ArrayList<>();
    list.add(1);
    list.add(2);
    //    3种循环方式 Iterator声明类型 ArrayList内部的一个类
    Iterator<Integer>iterator=list.iterator();//返回接口实现类的实例
    //  itit  迭代器的快捷键
    while (iterator.hasNext()){
        System.out.println(iterator.next());
    }
```
- ListIterator 的常用方法
  - add
  - hasNext
  - hasPrevious
  - next
  - nextIndex
  - previous
  - previousIndex
  - remove
  - set

### Utils  实用工具类接口
- `Collections 接口，给list，set，map 排序使用的`
    - reverse 反转
    - sort  排序 按元素的值排序
    - singletonList `ompare with Arrays.asList() `
- `Arrays 数组的工具类`
    - asList
    - binarySearch 实现二分查找 某一个值  前提是经过排序才可以 返回是排序后的结果的元素的索引
    - copyOf
    - copyOfRange
    - equals 判断是否相等 
    - fill  填充 数据全部改变
    - sort  排序
    - toString  输出全部数组
    - deepToString  二维数组以字符串形式输出
