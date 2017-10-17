
## 集合框架  很多接口和类的组合

> The `Java Collections Framework` is a collection of interfaces and classes which helps in storing and processing the data efficiently.

### Main Interfaces 接口之间的继承关系 
- `Iterable`
- `Collection`
  - `List` ctrl+alt+u  鼠标放在类的上面 出现继承图
  
    ![List](../image/javase/diagram/List.png)
  
  - `Set`
  
    ![Set](../image/javase/diagram/Set.png)
  
- `Map`

### List

> 有序（序列）有索引和下标 

> 可重复元素

- `Vector`
  
  ![Vector](../image/javase/diagram/Vector.png)
  
- **`ArrayList`最常用的 Java util 包**
  
  ![ArrayList](../image/javase/diagram/ArrayList.png)
  
  > constructors 3个构造器
  
  - ArrayList()  无参数构造方法
  - ArrayList(Collection<? extends E> c)
  - **ArrayList(int initicalCapacity) 推荐使用 没有取得容量的方法 但有容量的概念**
  
  > methods
  
  - **add**
  - **addAll 加入另一个集合的元素**
  - **size**
  - clear
  - contains 是否包含 返回是否
  - ensureCapacity 容量有关
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
   
  > extended methods  继承来的方法
  
  - equals
  - iterator
  - listIterator
  - subList [Converting a subList of an ArrayList to an ArrayList](http://stackoverflow.com/a/16644841/3414180)
  - containsAll
  - removeAll
  - removeIf `JDK 1.8`
  - retainAll [Why retainAll in ArrayList throws an Exception](http://stackoverflow.com/a/17564823/3414180)
  
- `LinkedList`
  
  ![LinkedList](../image/javase/diagram/LinkedList.png)
  
- ArrayList Vs LinkedList
  - Search: ArrayList search operation is pretty fast compared to the LinkedList search operation. get(int index) in ArrayList gives the performance of O(1) while LinkedList performance is O(n).

  > Reason: ArrayList maintains index based system for its elements as it uses array data structure implicitly which makes it faster for searching an element in the list. On the other side LinkedList implements doubly linked list which requires the traversal through all the elements for searching an element.

  - Deletion: LinkedList remove operation gives O(1) performance while ArrayList gives variable performance: O(n) in worst case (while removing first element) and O(1) in best case (While removing last element). Conclusion: LinkedList element deletion is faster compared to ArrayList.

  > Reason: LinkedList’s each element maintains two pointers (addresses) which points to the both neighbor elements in the list. Hence removal only requires change in the pointer location in the two neighbor nodes (elements) of the node which is going to be removed. While In ArrayList all the elements need to be shifted to fill out the space created by removed element.

  - Inserts Performance: LinkedList add method gives O(1) performance while ArrayList gives O(n) in worst case. Reason is same as explained for remove.

  - Memory Overhead: ArrayList maintains indexes and element data while LinkedList maintains element data and two pointers for neighbor nodes hence the memory consumption is high in LinkedList comparatively.
  