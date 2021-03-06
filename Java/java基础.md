# 基础

# 容器
# List
ArrayList和LinkedList的区别



# Set
HashSet 
HashSet实现了Set接口，由哈希表支持。它，特别是它不保证该顺序恒久不变。


TreeSet 
TreeSet整体上性能没有HashSet好，但是它可以维持元素的排序状态。
TreeSet底层使用的容器实际上就是TreeMap，它以TreeMap的key来保存set集合的元素，value都以一个名为PRESENT的Object对象代替（无实际意义）。

# Map
HashMap 
HashMap底层就是一个数组结构，数组中的每一项又是一个链表(其实就是哈希表的拉链法实现)。但是此类不保证映射的顺序，特别是不保证该顺序恒久不变。但是TreeMap可以维持映射的顺序。

Hashtable 
和HashMap实现差不多，Hashtable是线程安全的，它的实现方法里面都添加了synchronized关键字来确保线程同步。HashMap是线程不安全的，在多线程编程下如使用HashMap需要使用Collections.synchronizedMap()来获取一个线程安全的集合。譬如HashMap可以接受null键值和值，而Hashtable则不能

TreeMap 
TreeMap的底层实现是一个红黑树结构，这样可以保证快速检索节点，TreeMap可以维持映射的

# hash
两个对象就算hashcode相同，但是它们可能并不相等。因为hashcode相同，所以它们的bucket位置相同，‘碰撞’会发生。因为HashMap使用链表存储对象，这个Entry(包含有键值对的Map.Entry对象)会存储在链表中。
通过hashcode找到bucket位置之后，会调用keys.equals()方法去找到链表中正确的节点。采用合适的equals()和hashCode()方法的话，将会减少碰撞的发生，提高效率。
equal()相等的两个对象他们的hashCode()肯定相等，也就是用equal()对比是绝对可靠的。


# JVM 虚拟机
## 内存分配
1.程序计数器（ Program Counter Register）

程序计数器（ Program Counter Register）是一块较小的内存空间，它的作用可以看做是当前线程所执行的字节码的行号指示器。字节码解释器工作时就是通过改变这个计数器的值来选取下一条需要执行的字节码指令，分支、循环、跳转、异常处理、线程恢复等基础功能都需要依赖这个计数器来完成。字节码解释器工作时就是通过改变这个计数器的值来选取下一条需要执的字节码指令，分支、循环、跳转、异常处理、线程恢复等基础功能都需要依赖这个计数器来完成。该区域是属于线程私有的,因为在多线程环境中CPU通过在不同的线程来高速切换，此时程序计数器需要记录当前线程执行到哪一步了，以便下一次CPU可以在这个记录点上继续执行。 
此内存区域是唯一一个在Java 虚拟机规范中没有规定任何 OutOfMemoryError 情况的区域。

2 Java 虚拟机栈（ Java Virtual Machine Stacks）Java栈
java方法调用栈
在函数中定义的一些基本类型的变量和对象的引用变量都是在函数的栈内存中分配。当在一段代码块中定义一个变量时，java就在栈中为这个变量分配内存空间，当超过变量的作用域后，java会自动释放掉为该变量分配的内存空间，该内存空间可以立刻被另作他用。实际上，栈中的变量指向堆内存中的变量，这就是 Java 中的指针!

3.本地方法栈（ Native Method Stacks）

与虚拟机栈所发挥的作用是非常相似的，其区别不过是虚拟机栈为虚拟机执行 Java 方法（也就是字节码）服务，而本地方法栈则是为虚拟机使用到的 Native方法服务。一个Native Method就是一个Java调用非java代码的接口。一个Native Method是这样一个java的方法：该方法的实现由非java语言实现，比如C。

4.Java 堆（ Java Heap）

Java堆是 Java 虚拟机所管理的内存中最大的一块。 Java堆是被所有线程共享的一块内存区域，在虚拟机启动时创建。此内存区域的唯一目的就是存放对象实例，几乎所有的对象实例都在这里分配内存。Java 堆是垃圾收集器管理的主要区域，因此很多时候也被称做“GC 堆（ ” Garbage Collected Heap）。如果从内存回收的角度看，Java堆又会划分为好几个区域(新时代，老年代，等等)如果从内存分配的角度看，线程共享的 Java 堆中可能划分出多个线程私有的分配缓冲区。但无论怎么去划分，无论那个区域，java堆中存储的依然是对象的实例。进一步划分的目的是为了更好地回收内存，或者更快地分配内存。如果在堆中没有内存完成实例分配，并且堆也无法再扩展时，将会抛出 OutOfMemoryError 异常。

5.方法区（ Method Area）

与 Java 堆一样，是各个线程共享的内存区域，它用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。方法区是存放虚拟机加载类的相关信息，如类、静态变量和常量，大小由-XX:PermSize和-XX:MaxPermSize来调节，类太多有可能撑爆永久带：

## GC
1. 引用计数算法         给对象中添加一个引用计数器，每当有一个地方引用它时，计数器就加1；当引用失效时，计数器值就减1；任何时刻计数器都为0的对象就是不可能再被使用的。         Java语言没有选用引用计数法来管理内存，因为引用计数法不能很好的解决循环引用的问题。    
2. 根搜索算法       在主流的商用语言中，都是使用根搜索算法来判定对象是否存活的。       GC Root Tracing 算法思路就是通过一系列的名为"GC  Roots"的对象作为起始点，从这些节点开始向下搜索，搜索所走过的路径称为引用链（Reference Chain），当一个对象到GC Roots没有任何引用链相连，即从GC Roots到这个对象不可达，则证明此对象是不可用的。