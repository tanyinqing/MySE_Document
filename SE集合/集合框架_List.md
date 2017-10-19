
## 集合框架  很多接口和类的组合

> The `Java Collections Framework` is a collection of interfaces and classes which helps in storing and processing the data efficiently.

### Main Interfaces 接口之间的继承关系 
- `Iterable`
- `Collection`
  - `List` ctrl+alt+u  鼠标放在类的上面 出现继承图 放在包上显示包结构
  
    ![List](../image/javase/diagram/List.png)
  
  - `Set`
  
    ![Set](../image/javase/diagram/Set.png)
  
- `Map`

### List 蓝线是继承 绿线是接口

> 有序（序列）有索引和下标 

> 可存放重复元素 
> 机制是先建立一个数组， 

- `Vector`
  
  ![Vector](../image/javase/diagram/Vector.png)
  
- **`ArrayList`最常用的 Java util 包**
  
  ![ArrayList](../image/javase/diagram/ArrayList.png)
  
  > constructors 3个构造器
  
  - ArrayList()  无参数构造方法 初始容量是10
  - ArrayList(Collection<? extends E> c)
  - **ArrayList(int initicalCapacity) 推荐使用 没有取得容量的方法 但有容量的概念**
  
  > methods
  
  - **add**
  - **addAll 加入另一个集合的元素**
  - **size**
  - clear
  - contains 是否包含 返回是否
  - ensureCapacity 初始化容量的大小，提升效率
  - **get**
  - indexOf  返回元素的索引值 从前向后查找
  - isEmpty 判断集合是否为空
  - lastIndexOf 返回元素的索引值 从后向前查找
  - remove 删除 参数是索引
  - removeRange  受保护的方法，子类才可以访问，删除一个范围
  - set 修改
  - **size**
  - toArray  把它作为一个数组对象输出，看的更清楚了
  - trimToSize  把容量变成和size一样多
  
  ```
   ArrayList<Integer>integers=new ArrayList<>(10000);
          integers.add(1);
          integers.add(1);
          integers.add(1);
          System.out.println(integers);//[1, 1, 1]查看明细
          
          哈希码 为每个对象提供的一个编码
          
          for (OverrideTest overrideTest : overrideTests) {
                     System.out.println(overrideTest.hashCode());
                 } 一次输出对象的哈希码
                 
                  integers.trimToSize(); // capacity = size   把容量变成和size一样多
                 
       这是object中头string的源码  返回 cn.edu.tsinghua.javase.ceshi.OverrideTest@74a14482         
       前部分是包名   hashCode()这个是哈希码 Integer.toHexString这个是讲对象的哈希码转化成16进制
     public String toString() {
            return getClass().getName() + "@" + Integer.toHexString(hashCode());
        }
  ```
   
  > extended methods  继承来的方法
  
  - equals 两个列表个数一样 顺序一样才可以 ==比较的是内存的地址
  - iterator
  - listIterator
  - subList [Converting a subList of an ArrayList to an ArrayList](http://stackoverflow.com/a/16644841/3414180)
  - containsAll  一个链表是否全包含另一个链表
  - removeAll
  - removeIf `JDK 1.8`
  - retainAll  这里取的是交集部分
  [Why retainAll in ArrayList throws an Exception](http://stackoverflow.com/a/17564823/3414180)
  
- `LinkedList` 内部原理 静态数组 满了就扩容 双向链表 节点有前后双向
- prev nest上一个与下一个
  
  ![LinkedList](../image/javase/diagram/LinkedList.png)
  
- ArrayList Vs LinkedList  时空复杂度 LinkList 占的内存更大
  - Search: ArrayList search operation is pretty fast compared to the LinkedList search operation. get(int index) in ArrayList gives the performance of O(1) while LinkedList performance is O(n).
  - 找某一个元素，通过索引，ArrayList比较快，前后中时间差不多 LinKList 逐个比较找元素 两边快，中间慢
  > Reason: ArrayList maintains index based system for its elements as it uses array data structure implicitly which makes it faster for searching an element in the list. On the other side LinkedList implements doubly linked list which requires the traversal through all the elements for searching an element.

  - Deletion: LinkedList remove operation gives O(1) performance while ArrayList gives variable performance: O(n) in worst case (while removing first element) and O(1) in best case (While removing last element). Conclusion: LinkedList element deletion is faster compared to ArrayList.
  - 删除LinkList比较快 
  > Reason: LinkedList’s each element maintains two pointers (addresses) which points to the both neighbor elements in the list. Hence removal only requires change in the pointer location in the two neighbor nodes (elements) of the node which is going to be removed. While In ArrayList all the elements need to be shifted to fill out the space created by removed element.

  - Inserts Performance: LinkedList add method gives O(1) performance while ArrayList gives O(n) in worst case. Reason is same as explained for remove.
  - 加入一个元素，
  - Memory Overhead: ArrayList maintains indexes and element data while LinkedList maintains element data and two pointers for neighbor nodes hence the memory consumption is high in LinkedList comparatively.
  
  -ArrayLisst 删除一个，后面的元素移除前移
  -ListLisst 删除一个，上一个和下一个相互指向一下就可以了
  - ListLisst 用在频繁的修改和删除上
  
  ```
     // ArrayList 一万个元素 删除第一个需要的微秒数
          ArrayList<Integer>arrayList=new ArrayList<>();
          for (int i = 0; i < 1000000; i++) {
              arrayList.add(i);
          }
      long begin=System.nanoTime();//微秒s
          arrayList.remove(0);
          System.out.println(System.nanoTime()-begin);
  ```