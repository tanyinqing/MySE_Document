### Map

> `Key - Value` 对结构
  
- `Hashtable`
  
  > 无序

  > `non-null` and key `non-null` value
  
  ![Hashtable](../image/javase/diagram/Hashtable.png)
  
- `HashMap`

  > 无序
  
  > `null` key and `null` value
  
  ![HashMap](../image/javase/diagram/HashMap.png)
  
- `LinkedHashMap`

  > 使用 `Hashtable` 实现

  > 按元素添加顺序排序
  
  > `null` key and `null` value  
  
  ![LinkedHashMap](../image/javase/diagram/LinkedHashMap.png)
  
- `TreeMap`

  > 使用 `红-黑 树` 存储元素

  > 按元素值排序

  > `non-null` key and `null` value
  
  ![TreeMap](../image/javase/diagram/TreeMap.png)
  
- ~~`WeakHashMap`~~
  
  ![WeakHashMap](../image/javase/diagram/WeakHashMap.png)
  
- ~~`IdentityHashMap`~~
  
  ![IdentityHashMap](../image/javase/diagram/IdentityHashMap.png)

### Iterator / ListIterator

- `Iterator`
- `ListIterator`

  ![ListIterator](../image/javase/diagram/ListIterator.png)

#### Iterator Vs ListIetrator

- Iterator 可用于遍历 List 和 Set

  > ListIterator 只能遍历 List

- Iterator 只能向前遍历

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

### Utils
- `Collections`
    - reverse
    - sort
    - singletonList `ompare with Arrays.asList()`
- `Arrays`
    - asList
    - binarySearch
    - copyOf
    - copyOfRange
    - equals
    - fill
    - sort
    - toString
    - deepToString
