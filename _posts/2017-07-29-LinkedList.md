LinkedList 和 ArrayList 一样，都实现了 List 接口，但其内部的数据结构有本质的不同。LinkedList 是基于链表实现的（通过名字也能区分开来），所以它的插入和删除操作比 ArrayList 更加高效。但也是由于其为基于链表的，所以随机访问的效率要比 ArrayList 差。

#### LinkedList类定义  
```java
public class LinkedList<E>  extends AbstractSequentialList<E>  
    implements List<E>, Deque<E>, Cloneable,java.io.Serializable {

    //一些属性和方法

     transient int size = 0 //长度

     transient Node<E> first; //第一个节点

     transient Node<E> last; //最后一个节点
    //用于存储数据的私有静态内部类
     private static class Node<E> {
        ...
        }
    }

...




}
```
> LinkedList 继承自 AbstractSequenceList，实现了 List、Deque、Cloneable、java.io.Serializable 接口。AbstractSequenceList 提供了List接口骨干性的实现以减少实现 List 接口的复杂度，Deque 接口定义了双端队列的操作。
>
> 在 LinkedList 中除了本身自己的方法外，还提供了一些可以使其作为栈、队列或者双端队列的方法。这些方法可能彼此之间只是名字不同，以使得这些名字在特定的环境中显得更加合适。
>
> LinkedList 也是 fail-fast 的（前边提过很多次了）。

#### 重要方法源码

* 用于存放数据的私有静态内部类
```java
private static class Node<E> {
     E item;
     Node<E> next;
     Node<E> prev;

     Node(Node<E> prev, E element, Node<E> next) {
         this.item = element;
         this.next = next;
         this.prev = prev;
    }
}
```
> 可见一个节点Node中除了存放当前节点数据element,外还存放了前一个节点prev和后一个节点next的引用

* add()
```java
public boolean add(E e) {
    linkLast(e);
    return true;
}
//-----------------
/**
 * Links e as last element.
 */
void linkLast(E e) {
 final Node<E> l = last;
 final Node<E> newNode = new Node<>(l, e, null);
 last = newNode;
 if (l == null)
     first = newNode;
 else
     l.next = newNode;
 size++;
 modCount++;
}

//------------------

/**
 * Links e as first element.
 */
private void linkFirst(E e) {
    final Node<E> f = first;
    final Node<E> newNode = new Node<>(null, e, f);
    first = newNode;
    if (f == null)
        last = newNode;
    else
        f.prev = newNode;
    size++;
    modCount++;
}

//插入到指定位置
public void add(int index, E element) {
    checkPositionIndex(index);

    if (index == size)
        linkLast(element);
    else
        linkBefore(element, node(index));
}
//  ↓
void linkBefore(E e, Node<E> succ) {
    // assert succ != null;
    final Node<E> pred = succ.prev;
    final Node<E> newNode = new Node<>(pred, e, succ);
    succ.prev = newNode;
    if (pred == null)
        first = newNode;
    else
        pred.next = newNode;
    size++;
    modCount++;
}
```
>  add(E e)是继承与AbstractList的方法,没指定插入位置,默认是调用linkLast(E e)  插入到末尾位置.可见是新建了一个node,让后在存数据的同时prev属性指向了前一个node.   
add(int index, E element)  
插入到指定位置,插入数据和前后node引用之外,还更新前面node的next node,后一node的prev node

```java
public E get(int index) {
   checkElementIndex(index);
   return node(index).item;
}

//look ↓
/**
 * Returns the (non-null) Node at the specified element index.
 */
Node<E> node(int index) {
    // assert isElementIndex(index);

    if (index < (size >> 1)) {
        Node<E> x = first;
        for (int i = 0; i < index; i++)
            x = x.next;
        return x;
    } else {
        Node<E> x = last;
        for (int i = size - 1; i > index; i--)
            x = x.prev;
        return x;
    }
}
```

> 可见,若要访问某个位置的节点的数据,将会从头(或者尾)进行查到,相当于遍历到该数据的位置. if (index < (size >> 1)) 表明如果位置小于链表的一半则从头开始遍历,否则从后面开始倒序遍历
