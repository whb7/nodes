> 写在最前：这些都是面试的时候整理的题目，所有的题目来源于网上，几乎包含了Java面试所有的实体，自己进行了部分答案的编写。
> PS：小伙伴们如果有不懂的地方可以在评论进行留言，也可以对未作答的题目进行补充，我会持续进行更新。


## 结合另一篇文章食用更为妥当[【面试宝典】JUC部分（对应周阳老师的面试教程）](https://blog.csdn.net/weixin_43431766/article/details/107151265)


# **一、Java 基础**

### **1.JDK和JRE有什么区别**


JDK是Java Development Kit 的缩写，包含了Java开发的基础类库，开发环境和运行环境，主要面向开发人员

JRE是Java RunTime Environment的缩写，包含了Java的运行环境，主要面向用户



### **2.== 和 equals 的区别是什么？**

	== 作用于基本数据类型时，比较的是变量的值，作用于引用类型时，比较的是变量的地址

	equals只作用于引用类型，String和Data类重写了equals方法，所以一般比较的是变量的值


​

### **3.两个对象的 hashCode相同，则 equals也一定为 true，对吗？**

	不一定，hashCode比较的是哈希值，equals比较的是引用的地址

	hashCode和equals都是可以自定义的

	但是一般规定equals相等的变量，hashCode也要相等，equals不相等的变量，不要求hashCode一定相等

	所以在重写equals方法时也要修改hashCode方法


​

### **4.final 在 java 中有什么作用？**

	final主要修饰类，方法和变量

	在修饰类时，表示该类不可以被继承

	在修饰方法时，表示该方法不可以被重写

	在修饰变量时，表示对象的引用不能被修改，但是值可以被修改，因为内存地址中保存的值可以被改变，final	主要是保证改变变量值时，变量对应的内存地址是不变的



### **5.java 中的 Math.round(-1.5) 等于多少？**

	round是四舍六入五成双，对于五，则加0.5后取整  -1.5+0.5= -1


​

### **6.String 属于基础的数据类型吗？**

	不属于，Java总共有8种基本类型，除了基本数据类型都是引用数据类型

	整型：byte short int long

	浮点型：float double

	字符型：char

	布尔类型：boolean

	String是使用final修饰的引用类型



### **7.java 中操作字符串都有哪些类？它们之间有什么区别？**

	String  StringBuffer  StringBuilder

	String类使用final修饰，不能被更改，性能比较低，内存占用更高，每次使用都会New一个新的对象

	StringBuffer和StringBuilder加强了对字符串的操作，可以更改，但是StringBuffer使用了synchronized方法，	更加安全，适合多线程，如果是单线程可以使用StringBuilder



### **8.String str="i"与 String str=new String("i")一样吗？**（不熟悉）

	不一样，String str = "i"首先会在常亮池中去寻找有没有i，如果不存在，则开辟空间保存i，如果存在就不会开辟 	新的空间，而是在栈内存中开辟一个str的空间去存储i的地址值

	new String("i")也是会先查找有没有i，如果没有，开辟空间保存i，在运行时，通过String类的构造器在堆内存中	new了一个空间，然后将常量池中的i复制一份放到该堆中，在栈中开辟名为str的空间，存放堆中这个对象的地	址

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-BZxQ4SDD-1594003559111)(C:\Users\WHB\AppData\Roaming\Typora\typora-user-images\image-20200314150139851.png)]

	注：栈：为编译器自动分配和释放，如函数参数、局部变量、临时变量等等
			堆：为成员分配和释放，由程序员自己申请、自己释放。否则发生内存泄露。典型为使用new申请的堆内					容。



###  **9.如何将字符串反转？**

	使用SpringBuffer或StringBuilder的reverse方法，本质上调用的都是他们的父类AbstractStringBuilder

	或者自己实现，以递归写法为例

```java
public String reverseByRecursion(String str) {
    int length = str.length();
    if (length <= 1) {
    return str;
    }
    return reverseByRecursion(str.substring(1) ) + str.charAt(0);
}
```

### **10.String 类的常用方法都有那些？**

	字符串的获取：

		length() 获取长度

		charAt() 获取指定索引位置的值

		indexOf() 获取本字符首次出现的索引位置，如果没有返回-1

	字符串的截取：

		substring(int index) 截取从参数位置一直到最后

		substring(int begin,int end) 返回begin到end包含左边不包含右边

	字符串的转换：

		char[] toCharArray() 将当前字符串转化成字符数组

		replace() 将老字符串替换为新的字符串

	分割字符串：

		split(String regex) 按照参数的格式将字符串分割为若干部分，返回一个字符数组，参数可以是正则表达式



### **11.抽象类必须要有抽象方法吗？**1111

	不必须，抽象类不一定需要有抽象方法，但是有抽象方法的一定要是抽象类



### **12.普通类和抽象类有哪些区别？**1111

	抽象类必须要有abstract关键字来修饰

	抽象类不能被实例化

	抽象类可以有抽象方法，抽象方法只需要声明，不需要实现

	抽象方法不能被声明为静态的，不能使用private修饰，不能使用final修饰(final修饰的类不能被继承)



### **13.抽象类能使用 final 修饰吗？**

	不能  考察点：final关键字的作用



### **14.接口和抽象类有什么区别？**

	接口使用interface修饰，抽象类使用abstract修饰

	接口中均为抽象方法，抽象类中既可以有抽象方法也可以对方法进行实现

	接口要被类实现，抽象类要被类继承

	接口中的成员变量只能是static final类型的,遵从开放封闭原则(认为是要变化的东西，就放在你自己的实现中，不能放在接口中去，接口只是对一类事物的属性和行为更高层次的抽象。对修改关闭，对扩展(不同的实现		implements)开放，接口是对开闭原则的一种体现。)

	一个类可以继承一个抽象类，但是可以实现多个接口



### **15.java 中 IO 流分为几种？**

	分为两种，一种是字节流，一种是字符流

	每种流都有输入和输出，主要对应四个抽象类

	InputStrem OutputStrem Reader Writer

	字节流可以用于任何的对象，包括二进制对象，而字符流只能处理字符或者字符串



### **BIO、NIO、AIO 有什么区别？**

[实现过程详解](https://blog.csdn.net/anxpp/article/details/51512200?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)

	BIO：Bolck IO 同步阻塞式IO，数据的读写必须阻塞在下一个线程内等待其完成

					BIO模型模拟：创建ServerSocket设置监听端口,使用accept函数循环等待，如果有客户端连接则创建					一个线程进行处理

	NIO：Non-Bolck（NEW） IO 同步非阻塞式IO

				三大核心 Channel（通道） Buffer（缓冲区） Selector（选择器）

	AIO：Asynchronous IO 异步非阻塞式IO

- **同步：** 同步就是发起一个调用后，被调用者未处理完请求之前，调用不返回。
- **异步：** 异步就是发起一个调用后，立刻得到被调用者的回应表示已接收到请求，但是被调用者并没有返回结果，此时我们可以处理其他的请求，被调用者通常依靠事件，回调等机制来通知调用者其返回结果。
- **阻塞：** 阻塞就是发起一个请求，调用者一直等待请求结果返回，也就是当前线程会被挂起，无法从事其他任务，只有当条件就绪才能继续
- **非阻塞：** 非阻塞就是发起一个请求，调用者不用一直等着结果返回，可以先去干其他事情。



###  **17.Files的常用方法都有哪些？**

- Files.exists() 检测文件路径是否存在
- Files.createFile()创建文件
- Files.createDirectory()创建文件夹
- Files.delete() 删除文件或者目录
- Files.copy() 复制文件
- Files.move() 移动文件
- Files.size（）查看文件个数
- Files.read() 读取文件
- Files.write()写入文件

# **二、容器**

###**18.java 容器都有哪些？**

	java容器类类库的用途是"保存对象"。摘自: “Thinking in Java”

	数组,String,java.util下的集合容器

	数组长度限制为 Integer.Integer.MAX_VALUE

	String的长度限制: 底层是char 数组 长度 Integer.MAX_VALUE 线程安全的

	Collection接口下的List,Set,Queue.和Map

	List:存放有序,列表存储,元素可重复

	Set:无序,元素不可重复

	Map:无序,元素可重复

	[解析](https://www.cnblogs.com/williamjie/p/11458691.html)

	注：Integer.MAX_VALUE = 2的32次方-1

			第一位是符号位(0是正数，1是负数)，后面的31位是数字位，所以最大的正数是011111……111，0			      	        后面总共31个1，就是2的32次方-1


​

###**19.Collection 和 Collections 有什么区别？**1111

- Java.util.Collection是一个集合接口， 定义了一些集合操作的通用方法，如size(),isEmpty()等。

	   List,Set,Queue都继承了Collection类，该类的作用是为各个集合提供了统一的操作方式。

- Java.util.Collections是一个针对Collection 的工具类，包含了有关集合操作的各种静态方法，如排序搜索等。

- 静态方法和普通方法的主要区别：静态方法在创建对象前就可以使用了，非静态方法必须通过new出来的对象调用。 静态方法可以通过 类名::方法名直接调用。普通方法需要创建一个实例，也就是new一个对象，然后通过 对象名->方法名的方式来调用



###**20.List、Set、Map 之间的区别是什么？**

- List按线性方式存储，是有序的，Set和Map是无序的，但是LinkedHashSet按照元素的插入顺序进行排序，TreeMap根据键对其中的元素进行升序排序。

- List里的值可以重复，Set不允许有重复对象，Map是以键值对的形式存储的，不允许有重复的键，但是键值可以重复。

- List允许多个null元素，Set只允许有一个null元素,Map只允许出现一个空键，但允许出现多个空值。





###**21.HashMap 和 Hashtable 有什么区别？**

- HashMap  可以存储null值和null键，线程不安全，可以使用ConcurrentHashMap保证线程安全，锁分段技术(数组里存放的是Segment对象，每个对象里都保存了一个hashMap,在调用put方法时，只针对进行操作的segment进行加锁)

- HashTable 不能存储null，线程安全，实现线程安全时是在修改数据的时候锁住整个HashTable，效率低



###**22.如何决定使用 HashMap 还是 TreeMap？**

- HashMap是链式数组，可以快速的获取key对应的value，但是不支持排序，查询多的时候使用HashMap

- TreeMap底层是红黑树，是一颗自平衡的二叉树，如果需要一个有序的结果，就使用TreeMap



###**23.说一下 HashMap 的实现原理？**

HashMap本质上是基于哈希表（散列表）的Map接口实现，使用数组加链表进行存储，当使用put（key,value）方法添加数据时，它调用键对象的hashCode()方法返回一个hashCode用于找到bucket位置来存储Entry对象。

当使用get(key)方法查找数据时，还是首先计算键的hashCode值，然后在bucket中找到对应的位置，如果后面没有Entry，就返回null,如果有，就使用equals方法比较当前key和要查找的key，如果返回true，则查找成功，否则将一直查找到链表最后。

如果两个对象的hashCode相同，他们的bucket位置就会相同，就会产生碰撞（冲突），在冲突个数比较少的时候HashMap是使用拉链法来解决冲突的，多的时候使用红黑树，当我们使用get方法获取对象时，找到bucket位置之后，会调用keys.equals()方法去在链表中找到正确的节点



###**24.说一下 HashSet 的实现原理？**

HashSet是基于HashMap来实现的，默认构造函数是构建一个初始容量为16，负载因子为0.75的HashMap。



###**25.ArrayList 和 LinkedList 的区别是什么？**

ArrayList和LinkedList都是不安全的

ArrayList底层使用的是Object数组，LinkedList在JDK1.6之前使用的是双向链表，JDK1.7取消了循环

进行插入和删除时，ArrayList受元素位置的影响，如果在最后一个就需要遍历到最后一个，LinkedList因为使用的链表，所以插入和删除不受元素位置的影响



26.如何实现数组和 List 之间的转换？

###**27.ArrayList 和 Vector 的区别是什么？**

Vector是现成安全的，使用synchronized实现线程安全

数据容量增长时，Vector会增长原来的一倍，ArrayList会增长原来的0.5倍



###28.Array 和 ArrayList 有何区别？

###29.在 Queue 中 poll()和 remove()有什么区别？

###30.哪些集合类是线程安全的？

###31.迭代器 Iterator 是什么？

###32.Iterator 怎么使用？有什么特点？

###33.Iterator 和 ListIterator 有什么区别？

###34.怎么确保一个集合不能被修改？

# **三、多线程**

### 并行和并发有什么区别？

- 并发：一个处理器可以同时处理多个任务。这是逻辑上的同时发生。指同一时刻只能够执行一条指令，但是多条指令被快速的进行切换，给人造成了它们同时执行的感觉。但在微观来说，并不同同时进行的，只是划分时间段，分别进行执行。
- 并行：多个处理器同时处理多个不同的任务。这是物理上的同时发生。在同一时刻，有多条指令在多个处理器上同时执行。
- 有一个清晰地比喻：
  并发：一个人同时吃三个苹果。并行：三个人同时吃三个苹果。



### 线程和进程的区别？

- 进程是CPU调度的基本单位，线程是程序执行的基本单位
- 一个进程中可以有多个线程，且至少会有一个线程
- 进程拥有独立的内存空间，所以他更加的稳定。多个线程共享一个进程的内存空间，他们是资源共享的，所以切换交流更加的方便，同时因为进程拥有独立的内存空间，所以进程如果挂掉了，那么程序也就终止了，但是进程可以有多个，一个进程挂了，可以由另外的进程代替他的工作。
- 进程开销会很大，线程的开销比较小

### 守护线程是什么？

- java中线程种分为守护线程Daemon和用户线程User。可以通过Thread.setDaemon(true)设置为守护线程，但是必须在start之前调用。
- Daemon是为其他线程提供服务，如果全部用户线程结束，Daemon没有服务对象，也就没有继续运行程序的必要了。
  守护线程最典型的应用就是 GC (垃圾回收器)

- 当 JVM 中不存在任何一个正在运行的非守护线程时，则 JVM 进程即会退出

### 创建线程有哪几种方式？

- 继承Thread类

- 实现runnale接口

- 实现callable接口



### 说一下 runnable 和 callable 有什么区别？

- 两者最大的不同点是：实现Callable接口的任务线程能返回执行结果；而实现Runnable接口的任务线程不能返回结果
- runnable使用run方法，callable使用call 方法
- Runnable 接口 run 方法只能抛出运行时异常，且无法捕获处理；Callable 接口 call 方法允许抛出异常，可以获取异常信息



### **线程有哪些状态？**

- 新建状态：新建线程对象，并没有调用start()方法之前

- 就绪状态：调用start()方法之后线程就进入就绪状态，但是并不是说只要调用start()方法线程就马上变为当前线程，在变为当前线程之前都是为就绪状态。值得一提的是，线程在睡眠和挂起中恢复的时候也会进入就绪状态哦。

- 运行状态：线程被设置为当前线程，开始执行run()方法。就是线程进入运行状态

- 阻塞状态：线程被暂停，比如说调用sleep()方法后线程就进入阻塞状态

- 死亡状态：线程执行结束



### sleep() 和 wait() 有什么区别？

- 功能差不多,都用来进行线程控制，sleep()不释放同步锁,wait()释放同步缩

  - sleep只是将cpu释放给其他线程使用
  - wait直接释放锁

- 还有用法的上的不同是:sleep(milliseconds)可以用时间指定来使他自动醒过来,如果时间不到你只能调用interreput()来强行打断;wait()可以用notify()直接唤起



### notify()和 notifyAll()有什么区别？

- notify() ：唤醒一个处于等待状态的线程，在调用此方法的时候，并不能确切的唤醒某一个等待状态的线程，而是由JVM确定唤醒哪个线程，而且不是按优先级。

- notifyAll():唤醒所有处入等待状态的线程;并可以理解为把他们排进一个队列;只不过只有头部的线程获得了锁，才能运行;注意！！并不是给所有唤醒线程一个对象的锁，而是让它们竞争，当其中一个线程运行完就开始运行下一个已经被唤醒的线程，因为锁已经转移了。这个时候是否运行已经不是因为等待状态，而是处于runnning队列中



### 创建线程池有哪几种方式？

- newFixedThreadPool 每当提交一个任务就创建一个线程，直到达到线程池的最大数量

- newCachedThreadPool 可缓存的线程池，如果线程池的容量超过了任务数，自动回收空闲线程，任务增加时可以自动添加新线程，线程池的容量不限制

- newSingleThreadExecutor 单线程的线程池，线程异常结束，会创建一个新的线程，能确保任务按提交顺序执行

- [外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-hiFHF2My-1594003559113)(C:\Users\WHB\AppData\Roaming\Typora\typora-user-images\image-20200515113644088.png)]

- ThreadPoolExecutor是线程池的主要操作类，上图的三个分别为指定线程数，单一线程，自动扩容线程

  他们底层都是调用了ThreadPoolExecutor类的构造方法来实现



### 线程池都有哪些状态？

- 运行(RUNNING)：该状态下的线程池接收新任务并处理队列中的任务；线程池创建完毕就处于该状态，也就是正常状态；
- 关机(SHUTDOWN)：线程池不接受新任务，但处理队列中的任务；线程池调用shutdown()之后的池状态；
- 停止(STOP)：线程池不接受新任务，也不处理队列中的任务，并中断正在执行的任务；线程池调用shutdownNow()之后的池状态；
- 清理(TIDYING)：线程池所有任务已经终止，workCount(当前线程数)为0；过渡到清理状态的线程将运行terminated()钩子方法；
- 终止(TERMINATED)：terminated()方法结束后的线程池状态；





### 线程池中 submit()和 execute()方法有什么区别？

- submit()有返回值，execute没有返回值
- execute() 参数 Runnable ；submit() 参数 (Runnable) 或 (Runnable 和 结果 T) 或 (Callable)
- submit() 的返回值 Future 调用get方法时，可以捕获处理异常



### 在 java 程序中怎么保证多线程的运行安全？

- 原子性：一个或者多个操作在 CPU 执行的过程中不被中断的特性
- 可见性：一个线程对共享变量的修改，另外一个线程能够立刻看到
- 有序性：程序执行的顺序按照代码的先后顺序执行



### 三个线程T1,T2,T3，怎么保证顺序执行

使用join方法，会使别的线程

### 多线程锁的升级原理是什么？

- JVM优化synchronized的运行机制，当JVM检测到不同的竞争状态时，就会根据需要自动切换到合适的锁，这种切换就是锁的升级。升级是不可逆的，也就是说只能从低到高，也就是偏向-->轻量级-->重量级，不能够降级、



- 无锁：没有对资源进行锁定，所有的线程都能访问并修改同一个资源，但同时只有一个线程能修改成功，其他修改失败的线程会不断重试直到修改成功。



- 偏向锁：对象的代码一直被同一线程执行，不存在多个线程竞争，该线程在后续的执行中自动获取锁，降低获取锁带来的性能开销。偏向锁，指的就是偏向第一个加锁线程，该线程是不会主动释放偏向锁的，只有当其他线程尝试竞争偏向锁才会被释放。

  偏向锁的撤销，需要在某个时间点上没有字节码正在执行时，先暂停拥有偏向锁的线程，然后判断锁对象是否处于被锁定状态。如果线程不处于活动状态，则将对象头设置成无锁状态，并撤销偏向锁；

  如果线程处于活动状态，升级为轻量级锁的状态。



- 轻量级锁：轻量级锁是指当锁是偏向锁的时候，被第二个线程 B 所访问，此时偏向锁就会升级为轻量级锁，线程 B 会通过自旋的形式尝试获取锁，线程不会阻塞，从而提高性能。

  当前只有一个等待线程，则该线程将通过自旋进行等待。但是当自旋超过一定的次数时，轻量级锁便会升级为重量级锁；当一个线程已持有锁，另一个线程在自旋，而此时又有第三个线程来访时，轻量级锁也会升级为重量级锁。



- 重量级锁：指当有一个线程获取锁之后，其余所有等待获取该锁的线程都会处于阻塞状态。

  重量级锁通过对象内部的监视器（monitor）实现，而其中 monitor 的本质是依赖于底层操作系统的 Mutex Lock 实现，操作系统实现线程之间的切换需要从用户态切换到内核态，切换成本非常高。




### 什么是死锁？

- 所谓死锁，是指多个进程在运行过程中因争夺资源而造成的一种僵局，当进程处于这种僵持状态时，若无外力作用，它们都将无法再向前推进。 因此我们举个例子来描述，如果此时有一个线程A，按照先锁a再获得锁b的的顺序获得锁，而在此同时又有另外一个线程B，按照先锁b再锁a的顺序获得锁。如下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706104710390.png)

- 竞争资源，进程间推进顺序非法会产生死锁
- 死锁产生的四个必要条件
  - 互斥条件：进程要求对所分配的资源进行排它性控制，即在一段时间内某资源仅为一进程所占用。
  - 请求和保持条件：当进程因请求资源而阻塞时，对已获得的资源保持不放。
  - 不剥夺条件：进程已获得的资源在未使用完之前，不能剥夺，只能在使用完时由自己释放。
  - 环路等待条件：在发生死锁时，必然存在一个进程--资源的环形链。



### 怎么防止死锁？

- 资源一次性分配：一次性分配所有资源，这样就不会再有请求了：（破坏请求条件）

- 只要有一个资源得不到分配，也不给这个进程分配其他的资源：（破坏请保持条件）

- 可剥夺资源：即当某进程获得了部分资源，但得不到其它资源，则释放已占有的资源（破坏不可剥夺条件）

- 资源有序分配法：系统给每类资源赋予一个编号，每一个进程按编号递增的顺序请求资源，释放则相反（破坏环路等待条件）



### ThreadLocal 是什么？有哪些使用场景？

- 在同步机制中，通过对象的锁机制保证同一时间只有一个线程访问变量。

  而ThreadLocal则从另一个角度来解决多线程的并发访问。ThreadLocal会为每一个线程提供一个独立的变量副本，从而隔离了多个线程对数据的访问冲突。

  ThreadLocal在每个本地线程中创建了一个ThreadLocalMap对象，每个线程可以访问自己内部ThreadLocalMap对象里的value。通过这种方式，实现线程之间的数据隔离。

- 为每个线程分配一个JDBC连接的Connection。这样可以保证每个线程都在各自的Connection上进行数据库的操作，不会出现A线程关闭了线程B正在使用的Connection



### 说一下 synchronized 底层实现原理？1111

每个对象有一个监视器锁（monitor）。当monitor被占用时就会处于锁定状态，线程执行monitorenter指令时尝试获取monitor的所有权，过程如下：

- 如果monitor的进入数为0，则该线程进入monitor，然后将进入数设置为1，该线程即为monitor的所有者。

- 如果线程已经占有该monitor，只是重新进入，则进入monitor的进入数加1.

- 如果其他线程已经占用了monitor，则该线程进入阻塞状态，直到monitor的进入数为0，再重新尝试获取monitor的所有权。



### synchronized 和 volatile 的区别是什么？

- synchronized 可以作用于变量、方法、对象；volatile 只能作用于变量。
- synchronized 可以保证线程间的有序性（猜测是无法保证线程内的有序性，即线程内的代码可能被 CPU 指令重排序）、原子性和可见性；volatile 只保证了可见性和有序性，无法保证原子性。
- synchronized 线程阻塞，volatile 线程不阻塞。



### **synchronized 和 Lock 有什么区别？**

两者区别：

1.首先synchronized是java内置关键字，在jvm层面，他底层是通过monitor对象来完成的，Lock是个java类；

2.synchronized无法判断是否获取锁的状态，Lock可以判断是否获取到锁；

3.synchronized会自动释放锁(a 线程执行完同步代码会释放锁 ；b 线程执行过程中发生异常会释放锁)，Lock需在finally中手工释放锁（unlock()方法释放锁），否则容易造成线程死锁；

4.用synchronized不可中断，除非抛出异常或正常运行完成，ReentrantLock可以中断，设置超时方法trylock

5.synchronized的锁可重入、不可中断、非公平，而Lock锁可重入、可判断、可公平（两者皆可）

6.Lock锁适合大量同步的代码的同步问题，synchronized锁适合代码少量的同步问题。



### synchronized 和 ReentrantLock 区别是什么？

- synchronized 是Java中的关键字，ReentrantLock是类，这是二者本质区别。既然 ReentrantLock 是类，那么它就提供了比synchronized 更多灵活的特性，可以被继承、可以有方法、可以有各种各样的类变量

- ReentrantLock 比synchronized 的扩展性体现在几点上：

  - ReentrantLock 可以对获取锁的等待时间进行设置，这样就避免了死锁发生
  - ReentrantLock 可以获取各种锁的信息
  - ReentrantLock 可以灵活的实现多路通知



### **说一下 atomic 的原理？**

1、直接操作内存，使用Unsafe 这个类

2、使用 getIntVolatile(var1, var2) 获取线程间共享的变量

3、采用CAS的尝试机制（核心所在）

```java
 public final int getAndAddInt(Object var1, long var2, int var4) {
        int var5;
        do {
            var5 = this.getIntVolatile(var1, var2);
        } while(!this.compareAndSwapInt(var1, var2, var5, var5 + var4));

        return var5;
    }
```

4、使用Atomic ，是在硬件上、寄存器进行阻塞，而不是在线程、代码上阻塞。



### **请谈一下你堆volatile的理解**

- volatile是java虚拟机提供的轻量级的同步机制，他主要有三大特性
  - 保证可见性
    - 其实就是JMM中的通知机制，线程的操作可以相互通知
  - 不保证原子性
    - 原子性：某个线程正在做具体业务时，中间不可以被加塞，需要整体完成，要么一起成功，要么一起失败
    - 解决方案：使用atomic类，主要是使用unsafe类+CAS
  - 禁止指令重排
    -![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706104735704.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



### **谈谈JMM**

- JMM是Java Memory Model的简称，他本身是一种抽象的概念，并不是真实存在的，他描述的是一组规则或规范
- JMM对于同步的规定：
  - 线程解锁前，必须把共享变量的值刷新回主内存
  - 线程加锁前，必须读取主内存的最新值到自己的空间
  - 加锁和解锁是同一把锁

- JVM运行程序的实体是线程，每一个线程创建的时候JVM都会为其创建一个工作内存，工作内存是每个线程的私有数据区域，而Java内存模型中规定所有的变量都要存储到主内存，主内存是共享内存区域的，每一个线程都可以访问，但线程对变量的操作必须在工作内存中进行，首先要将变量从工作内存中拷贝到自己的工作空间，然后对变量进行操作，操作完成后再将值存入到主内存，因此不同线程间无法访问对方的工作内存，线程间的通信必须通过主内存来完成

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706104753806.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



### **CAS是什么**

- 主要是进行比较并交换
  - ComparAndSwap，这个方法有两个参数，一个是expect,一个是update，原理是将主物理内存中的值跟期望值进行比较，如果相同，则修改为更新值，返回True
- CAS底层原理
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706104804710.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706104822211.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)
- CAS缺点
  - 循环时间长，开销大（因为do while）
  - 只能保证一个共享变量的原子操作，而synchronized可以保证整个方法
  - 引出来ABA问题



### **ABA问题**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706104834589.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

- 解决ABA问题（原子引用）
  - 使用AtomicReference<V>可以自定义原子类
  - 增加一个版本号，类似于时间戳，使用AtomicStampedReference<V>类
  - AtomicStampedReference<V>有四个参数
    - 期望值
    - 修改值
    - 期望版本号
    - 修改版本号



### 公平锁/非公平锁/可重入锁/递归锁/自旋锁

- 公平锁：是指多个线程按照申请锁的顺序来获取锁，类似排队打饭，先来后到



- 非公平锁：是指多个线程获取锁的顺序并不按照申请顺序，有可能后申请的线程比先申请的线程优先获取锁，在高并发情况下，有可能会造成优先级反转或者饥饿现象![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706104855122.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



- 可重入锁![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706104906141.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

  - ReentrantLock/Synchronized就是一个典型的可重入锁

  - 最大的作用是避免死锁



- 自旋锁

  - ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706104918271.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



- 独占锁/共享锁/互斥锁
  - ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706104927672.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)





### 阻塞队列用过吗

- 简单来说
  - 当阻塞队列是空的时候，从队列里获取元素的操作是阻塞的
  - 当阻塞队列是满的时候，往队列里添加元素的操作是阻塞的
- 他的好处是，我们不再需要关心什么时候需要阻塞线程，什么时候需要唤醒线程





# **四、反射**

### 什么是反射？

- 将类的各个组成部分封装为其他对象的过程，他的好处是可以在程序运行中，操作这些对象，可以解耦，提高程序的可扩展性，一句话来概括：反射就是把Java类中的各种成分映射成一个个的java对象

   （其实：一个类中这些成员方法、构造方法、在加入类中都有一个类来描述）

- 如图是类的正常加载过程：反射的原理在与class对象。Class对象的由来是将class文件读入内存，并为之创建一个Class对象![img](https://img-blog.csdn.net/20170513133210763)



- 获取Class对象的三种方式：
  - Class.forName(“全类名”)：将字节码文件加载进内存，返回Class对象
  - 类名.class：通过类名的属性class获取
  - 对象.getClass()：此方法再Object类种定义
  - 同一个字节码文件在一次程序运行过程中，只会被加载一次
  - ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706104943198.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

### 什么是 java 序列化？什么情况下需要序列化？

- 序列化：将 Java 对象转换成字节流的过程。

  反序列化：将字节流转换成 Java 对象的过程

- 序列化的实现：类实现 Serializable 接口，这个接口没有需要实现的方法。实现 Serializable 接口是为了告诉 jvm 这个类的对象可以被序列化

- 当 Java 对象需要在网络上传输 或者 持久化存储到文件中时，就需要对 Java 对象进行序列化处理。

### 59.动态代理是什么？有哪些应用？

- 代理模式是Java常见的设计模式之一。所谓代理模式是指客户端并不直接调用实际的对象，而是通过调用代理，来间接的调用实际的对象。开闭原则，增加功能
- 静态代理：
  - 静态代理的局限在于运行前必须编写好代理类
  - 如果接口改了，代理的也要跟着改
  - 因为代理对象，需要与目标对象实现一样的接口。所以会有很多代理类，类太多。
- 动态代理：
  - 代理对象，不需要实现接口【就不会有太多的代理类了】
  - 代理对象的生成，是利用JDKAPI， 动态地在内存中构建代理对象
  - 代理类需要实现InvocationHandler接口，实现invoke方法，通过Proxy类的newProxyInstance方法来创建代理对象



### 60.怎么实现动态代理？

一个典型的动态代理创建对象过程可分为以下四个步骤：
1、通过实现InvocationHandler接口创建自己的调用处理器 IvocationHandler handler = new InvocationHandlerImpl(...);
2、通过为Proxy类指定ClassLoader对象和一组interface创建动态代理类
Class clazz = Proxy.getProxyClass(classLoader,new Class[]{...});
3、通过反射机制获取动态代理类的构造函数，其参数类型是调用处理器接口类型
Constructor constructor = clazz.getConstructor(new Class[]{InvocationHandler.class});
4、通过构造函数创建代理类实例，此时需将调用处理器对象作为参数被传入
Interface Proxy = (Interface)constructor.newInstance(new Object[] (handler));
为了简化对象创建过程，Proxy类中的newInstance方法封装了2~4，只需两步即可完成代理对象的创建。
生成的ProxySubject继承Proxy类实现Subject接口，实现的Subject的方法实际调用处理器的invoke方法，而invoke方法利用反射调用的是被代理对象的的方法（Object result=method.invoke(proxied,args)）



### 讲讲JAVA的反射机制

简单来说，反射机制就是通过类名可以获取到这个类的所有信息。

在我们New 一个对象的时候，会生成一个.class文件，jvm会加载这个文件到jvm内存中生成一个Class对象，这个Class对象相当于是一个类的模板，且只会生成一次，再次新建对象的时候也是使用这个模板去创建，反射其实本质就是通过Class文件去方向的获取类的各种信息。

在实际开发中，经常使用Class.forname(“全限定类名”)方法获取Class对象，Spring框架的IOC机制就是使用的反射机制

# **五、对象拷贝**

61.为什么要使用克隆？

62.如何实现对象克隆？

63.深拷贝和浅拷贝区别是什么？

# **六、Java Web**

### 64.jsp 和 servlet 有什么区别？

- Servlet：

  Servlet 是一种服务器端的Java应用程序，具有独立于平台和协议的特性，可以生成动态的Web页面。它担当客户请求（Web浏览器或其他HTTP客户程序）与服务器响应（HTTP服务器上的数据库或应用程序）的中间层。 Servlet是位于Web服务器内部的服务器端的Java应用程序，与传统的从命令行启动的Java应用程序不同，Servlet由Web服务器进行加载，该Web服务器必须包含支持Servlet的Java虚拟机。



- Jsp：
  JSP 全名为Java Server Pages，中文名叫java服务器页面，其根本是一个简化的Servlet设计。JSP技术使用Java编程语言编写类XML的tags和scriptlets，来封装产生动态网页的处理逻辑。网页还能通过tags和scriptlets访问存在于服务端的资源的应用逻辑。JSP将网页逻辑与网页设计的显示分离，支持可重用的基于组件的设计，使基于Web的应用程序的开发变得迅速和容易。 JSP(JavaServer Pages)是一种动态页面技术，它的主要目的是将表示逻辑从Servlet中分离出来。

- 相同点

  jsp经编译后就变成了servlet，jsp本质就是servlet，jvm只能识别java的类，不能识别jsp代码，web容器将jsp的代码编译成jvm能够识别的java类



65.jsp 有哪些内置对象？作用分别是什么？

### 66.说一下 jsp 的 4 种作用域？

**四个作用域：request域 session域 application域 page域**

application：
全局作用范围，整个应用程序共享，就是在部署文件中的同一个webApp共享，生命周期为：应用程序启动到停止。



session：
会话作用域，当用户首次访问时，产生一个新的会话，以后服务器就可以记住这个会话状态。生命周期：会话超时，或者服务器端强制使会话失效。



request：
请求作用域，就是客户端的一次请求。



page：
一个JSP页面。

#### 67.session 和 cookie 有什么区别？

- cookie数据存放在客户的浏览器上，session数据放在服务器上。

- cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗
     考虑到安全应当使用session。

- session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能考虑到减轻服务器性能方面，应当使用COOKIE。

- 单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。

- 所以个人建议：将登陆信息等重要信息存放为SESSION。其他信息如果需要保留，可以放在COOKIE中



68.说一下 session 的工作原理？

69.如果客户端禁止 cookie 能实现 session 还能用吗？

70.spring mvc 和 struts 的区别是什么？

### 71.如何避免 sql 注入？

 SQL注入是比较常见的网络攻击方式之一，它不是利用操作系统的BUG来实现攻击，而是针对程序员编程时的疏忽，通过SQL语句，实现无帐号登录，甚至篡改数据库。



72.什么是 XSS 攻击，如何避免？

73.什么是 CSRF 攻击，如何避免？

# **七、异常**

74.throw 和 throws 的区别？

75.final、finally、finalize 有什么区别？

76.try-catch-finally 中哪个部分可以省略？

### 77.try-catch-finally 中，如果 catch 中 return 了，finally 还会执行吗？

- try 或 catch 中都有 return语句，并且有 finally 的话，最终先执行 finally，再执行 try 或 catch中的 return语句

- try 或 catch 中都有 return语句，并且有 finally，而且 finally中 有return语句 的话，最终先执行 finally，然后执行 finally中 有return语句，并不会执行 try 或 catch 中return语句

- try 或 catch 中都有 return语句，并且有 finally，而且 finally中 对try 或 catch 中的 return语句所返回的基本类型变量/引用类型变量 进行了重新赋值，即使如此，也只会返回 try 或 catch 中的return语句所返回的基本类型变量/引用类型变量的值，finally中的修改try 或 catch 中的返回值操作并不会生效



### 常见的异常类有哪些？

- 异常非常多，Throwable 是异常的根类。
- Throwable 包含子类 错误-Error 和 异常-Exception 。
- Exception 又分为 一般异常和运行时异常 RuntimeException

# **八、网络**

79.http 响应码 301 和 302 代表的是什么？有什么区别？

### forward 和 redirect 的区别？

- 是servlet种的两种主要的跳转方式。forward又叫转发，redirect叫做重定向
- 从地址栏显示来说：
  1. forword是服务器内部的重定向，服务器直接访问目标地址的 url网址，把里面的东西读取出来，但是客户端并不知道，因此用forward的话，客户端浏览器的网址是不会发生变化的。
  2. redirect是服务器根据逻辑，发送一个状态码，告诉浏览器重新去请求那个地址，所以地址栏显示的是新的地址。
- 从数据共享来说：

  1. 由于在整个定向的过程中用的是同一个request，因此forward会将request的信息带到被重定向的jsp或者servlet中使用。即可以共享数据
  2. redirect不能共享
- 从运用的地方来说
  1. forword 一般用于用户登录的时候，根据角色转发到相应的模块
  2. redirect一般用于用户注销登录时返回主页面或者跳转到其他网站

- 从效率来说：

  	forword效率高，而redirect效率低

- 从本质来说：

  	forword转发是服务器上的行为，而redirect重定向是客户端的行为





### 简述 tcp 和 udp的区别？

- **UDP是面向无连接的通讯协议，UDP数据包括目的端口号和源端口号信息。**

  - 优点：UDP速度快、操作简单、要求系统资源较少，由于通讯不需要连接，可以实现广播发送
    缺点：UDP传送数据前并不与对方建立连接，对接收到的数据也不发送确认信号，发送端不知道数
    据是否会正确接收，也不重复发送，不可靠。

- **TCP是面向连接的通讯协议，通过三次握手建立连接，通讯完成时四次挥手**

  - 优点：TCP在数据传递时，有确认、窗口、重传、阻塞等控制机制，能保证数据正确性，较为可靠。
    缺点：TCP相对于UDP速度慢一点，要求系统资源较多。



### tcp 为什么要三次握手，两次不行吗？为什么？

- 为了实现可靠数据传输， TCP 协议的通信双方， 都必须维护一个序列号， 以标识发送出去的数据包中， 哪些是已经被对方收到的。 三次握手的过程即是通信双方相互告知序列号起始值， 并确认对方已经收到了序列号起始值的必经步骤
- 如果只是两次握手， 至多只有连接发起方的起始序列号能被确认， 另一方选择的序列号则得不到确认



83.说一下 tcp 粘包是怎么产生的？

84.OSI 的七层模型都有哪些？

### get 和 post 请求有哪些区别？

Get是不安全的，因为在传输过程，数据被放在请求的URL中；Post的所有操作对用户来说都是不可见的。2.Get传送的数据量较小，这主要是因为受URL长度限制；Post传送的数据量较大，一般被默认为不受限制



#### HTTP和HTTPS有什么区别

1. https协议需要到ca申请证书，一般免费证书较少，因而需要一定费用。
2. http是超文本传输协议，信息是明文传输，https则是具有安全性的ssl加密传输协议。
3. http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。
4. http的连接很简单，是无状态的；HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全



HTTPS采用非对称加密和对称加密两种加密方式来保证传输信息的安全性：

非对称加密：用公钥和私钥来加解密（有同学这里不懂的话可以看看资料）。

对称加密：加密解密都用同一套秘钥。

注：非对称加密更加安全，对称加密速度更快。



https的请求流程：

1. 客户端（浏览器）向服务器请求https连接。

2. 服务器返回证书（公钥）到客户端。

3. 客户端随机的秘钥A（用于对称加密）。

4. 客户端用公钥对A进行加密。

5. 客户端将加密A后的密文发送给服务器。

6. 服务器通过私钥对密文进行解密得到对称加密的秘钥。

7. 客户端与服务器通过对称秘钥加密的密文通信。



上述过程中第2步骤中是存在风险的，因为公钥是暴露出来的，当公钥被中间人非法截获时，同时将公钥替换成中间人自己的公钥发送给客户端，从而得到对称加密的秘钥，进而伪装与客户端通信。



为了解决这种问题，就引入了数字证书与数字签名

所以在第2步骤时，服务器发送了一个SSL证书给客户端，SSL证书中包含了具体的内容有证书的颁发机构、有效期、公钥、证书持有者、签名，通过第三方的校验保证身份的合法。

一、首先客户端会读取证书所有者、有效期等信息进行校验。

二、客户端（浏览器）开始查找操作系统中已内置的受信任的证书发布机构CA，与服务器发过来的证书的颁发CA比对，用于验证证书是否为合法机构颁发。

三、如果找不到，浏览器就会报错。

四、如果找到了，就会取出其中的公钥，对证书内的签名进行解密。

五、使用相同的Hash算法对签名进行去摘要并与服务器发来的摘要进行对比。

六、如果对比一致，则合法，这样就得到公钥了



86.如何实现跨域？

87.说一下 JSONP 实现原理？

# **九、设计模式**

88.说一下你熟悉的设计模式？

### 89.简单工厂和抽象工厂有什么区别？

- 简单工厂，将对象的创建都交给工厂去进行，根据传入的参数，使用Switch或者if判断去进行实现具体的创建方法
- 工厂方法模式，其实就是对每一个对象，都编写一个工厂类，通过调用不同的工厂类创建不同的对象
- 抽象工厂，就是对工厂类进行加工，增加新的方法，去制造不同类型的对象
- 前面两种本质上都是对同一类对象进行生成，抽象工厂适合一个



### **设计模式的六大原则**

- **总原则：开闭原则（Open Close Principle）**

  开闭原则就是说对扩展开放，对修改关闭。在程序需要进行拓展的时候，不能去修改原有的代码，而是要扩展原有代码，实现一个热插拔的效果。所以一句话概括就是：为了使程序的扩展性好，易于维护和升级。想要达到这样的效果，我们需要使用接口和抽象类等

- **单一职责原则**

  也就是说每个类应该实现单一的职责，如若不然，就应该把类拆分

- **里氏替换原则**

  通俗点讲，只要父类能出现的地方子类就可以出现，而且替换为子类也不会产生任何错误或异常，使用者可能根本就不需要知道是父类还是子类。但是，反过来就不行了，有子类出现的地方，父类未必就能适应

- **依赖倒转原则**

  这个是开闭原则的基础，具体内容：面向接口编程，依赖于抽象而不依赖于具体。写代码时用到具体类时，不与具体类交互，而与具体类的上层接口交互。

- **接口隔离原则**

  每个接口中不存在子类用不到却必须实现的方法，如果不然，就要将接口拆分。使用多个隔离的接口，比使用单个接口（多个接口方法集合到一个的接口）要好

- **迪米特法则（最少知道原则）**

  一个类对自己依赖的类知道的越少越好。也就是说无论被依赖的类多么复杂，都应该将逻辑封装在方法的内部，通过public方法提供给外部。这样当被依赖的类变化时，才能最小的影响该类。

- **合成复用原则**

  尽量首先使用合成/聚合的方式，而不是使用继承



# **十、Spring/Spring MVC**

### **为什么要使用 spring？**

Spring 是一个轻量级IOC和AOP的容器框架，利用IOC降低了代码的耦合度



### 解释一下什么是 aop？

面向切面编程，主要使用的是动态代理的思想，动态代理是代理模式的一种，代理模式是指不直接调用对象，而是通过代理来间接的调用实际的对象，这样做的好处是，可以在不修改原始类的基础上，为原来的类添加功能，比如事务，日志等功能。

Spring AOP是基于动态代理的，如果要代理的对象实现了某个接口，那么Spring AOP就会使用JDK动态代理去创建代理对象；而对于没有实现接口的对象，就无法使用JDK动态代理，转而使用CGlib动态代理生成一个被代理对象的子类来作为代理

### 解释一下什么是 ioc？

控制反转，将类的创建和销毁等过程交给Spring容器来管理，使用反射机制，通过反射来获取对象

IOC容器实际上就是一个Map(key, value)，Map中存放的是各种对象，需要的时候将资源从Map中取出。主要作用是降低代码的耦合度，在开发中，并不能完全的消除耦合，只能降低耦合，一般保证编译期不出错（运行期可以出错）就可以了



### spring 有哪些主要模块？

**1、核心容器(Core)**

这是Spring框架最基础的部分，它提供了依赖注入（Dependency Injection）特征来实现容器对Bean的管理。这里最基本的概念是BeanFactory，它是任何Spring应用的核心。BeanFactory是工厂模式的一个实现，它使用IoC将应用配置和依赖说明从实际的应用代码中分离出来。

**2、AOP模块**

AOP即面向切面编程技术，Spring在它的AOP模块中提供了对面向切面编程的丰富支持。AOP允许通过分离应用的业务逻辑与系统级服务（例如安全和事务管理）进行内聚性的开发。应用对象只实现它们应该做的——完成业务逻辑——仅此而已。它们并不负责其它的系统级关注点，例如日志或事务支持。

**3、对象/关系映射集成模块ORM**

Hibernate是成熟的ORM产品，Spring并没有自己实现ORM框架而是集成了几个流行的ORM产品如Hibernate、JDO和iBATIS等。可以利用Spring对这些模块提供事务支持等。

**4、JDBC抽象和DAO模块**

Spring虽然集成了几个ORM产品，但也可以不选择这几款产品，因为Spring提供了JDBC和DAO模块。该模块对现有的JDBC技术进行了优化。你可以保持你的数据库访问代码干净简洁，并且可以防止因关闭数据库资源失败而引起的问题。

[JDBC DAO 抽象层提供了有意义的异常层次结构，可用该结构管管理异常处理和不同数据库供应商抛出的错误消息。异常层次结构简化了错误处理，并且极大地降低了需要编写的异常代码数量（例如打开和关闭连接）。SpringDAO的面向JDBC的异常遵从从通用的DAO异常层次结构]

**5、Spring的Web模块**

Web上下文模块建立于应用上下文模块之上，提供了一个适合于Web应用的上下文。另外，这个模块还提供了一些面向服务支持。例如：实现文件上传的multipart请求，它也提供了Spring和其它Web框架的集成，比如Struts、WebWork。

**6、应用上下文（Context）模块**

核心模块的BeanFactory使Spring成为一个容器，而上下文模块使它成为一个框架。Web上下文模块建立于应用上下文模块之上，提供了一个适合于Web应用的上下文。该模块还提供了一些面向服务支持这个模块扩展了BeanFactory的概念，增加了对国际化（I18N）消息、事件传播以及验证的支持。

另外，这个模块还提供了许多企业服务，例如电子邮件、JNDI访问、EJB集成、远程以及时序调度（scheduling）服务。也包括对模版框架例如Velocity和FreeMarker集成的支持。

**7、Spring的MVC框架**

Spring为构建Web应用提供了一个功能全面的MVC框架。虽然Spring可以很容易地与其它MVC框架集成，例如Struts2，但Spring的MVC框架使用IoC对控制逻辑和业务对象提供了完全的分离。



### BeanFactory和FactoryBean的区别

 BeanFactory是接口，提供了OC容器最基本的形式，给具体的IOC容器的实现提供了规范，

  FactoryBean也是接口，为IOC容器中Bean的实现提供了更加灵活的方式，FactoryBean在IOC容器的基础上给Bean的实现加上了一个简单工厂模式和装饰模式(如果想了解装饰模式参考：[修饰者模式(装饰者模式，Decoration)](https://www.cnblogs.com/aspirant/p/9083082.html) 我们可以在getObject()方法中灵活配置。其实在Spring源码中有很多FactoryBean的实现类.



### spring 常用的注入方式有哪些？

- 构造方法注入
  - 使用的标签：construtor-arg
  - 属性
    - type:用于指定要注入的数据类型
    - index:用于指定要注入数据的索引位置
    - name:用于指定给构造函数中的名称
    - ref:引用关联的bean对象
- setter注入
  - 使用的标签：property
  - 属性 name,value,ref
- 注解注入
  - 用于注入Bean @Component
    - 作用：用于把当前类对象存入Spring中
    - 属性：
      - value:用于指定Bean的id，默认是当前类名首字母小写
    - 需要在bean.xml中指定需要扫描的包
  - 用于注入数据 @AutoWrite
    - 自动按照数据类型注入，如果有多个匹配时，会使用变量名称在该类型中查找
    - @Qualifier组合  填写id
    - @Resourec 直接使用name属性按照bean的id注入
  - @Value
    - 作用：用于注入基本类型和String类型的数据



### 常用注解

- @Configuration配置类
- @ComponentScan ：指定spring容器时扫描的包

- @Bean 将方法的返回值存入Spring容器中

- @Import 用于导入其他配置类



### spring 中的 bean 是线程安全的吗？

大部分时候我们并没有在系统中使用多线程，所以很少有人会关注这个问题。单例bean存在线程问题，主要是因为当多个线程操作同一个对象的时候，对这个对象的非静态成员变量的写操作会存在线程安全问题。

有两种常见的解决方案：

1.在bean对象中尽量避免定义可变的成员变量（不太现实）。

2.在类中定义一个ThreadLocal成员变量，将需要的可变成员变量保存在ThreadLocal中（推荐的一种方式）



### 96.spring 支持几种 bean 的作用域？

- singleton：单例模式，在整个Spring IoC容器中，使用 singleton 定义的 bean 只有一个实例
- prototy：原型模式，每次通过容器的getbean方法获取 prototype 定义的 bean 时，都产生一个新的 bean 实例
- request：对于每次 HTTP 请求，使用 request 定义的 bean 都将产生一个新实例，即每次 HTTP 请求将会产生不同的 bean 实例
- session：同一个 Session 共享一个 bean 实例。
- global-session：作用于集群环境的会话范围![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105056843.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)







### 97.spring 自动装配 bean 有哪些方式？

- ByName
- ByType
- Constructor
- Autodetect
- no



### Spring Bean 的生命周期

  在说明前可以思考一下Servlet的生命周期：实例化，初始init，接收请求service，销毁destroy；

  Spring上下文中的Bean也类似，如下

  1、实例化一个Bean－－也就是我们常说的new；

  2、按照Spring上下文对实例化的Bean进行配置－－也就是IOC注入；

  3、如果这个Bean已经实现了BeanNameAware接口，会调用它实现的setBeanName(String)方法，此处传递的就是Spring配置文件中Bean的id值

  4、如果这个Bean已经实现了BeanFactoryAware接口，会调用它实现的setBeanFactory(setBeanFactory(BeanFactory)传递的是Spring工厂自身（可以用这个方式来获取其它Bean，只需在Spring配置文件中配置一个普通的Bean就可以）；

  5、如果这个Bean已经实现了ApplicationContextAware接口，会调用setApplicationContext(ApplicationContext)方法，传入Spring上下文（同样这个方式也可以实现步骤4的内容，但比4更好，因为ApplicationContext是BeanFactory的子接口，有更多的实现方法）；

  6、如果这个Bean关联了BeanPostProcessor接口，将会调用postProcessBeforeInitialization(Object obj, String s)方法，BeanPostProcessor经常被用作是Bean内容的更改，并且由于这个是在Bean初始化结束时调用那个的方法，也可以被应用于内存或缓存技术；

  7、如果Bean在Spring配置文件中配置了init-method属性会自动调用其配置的初始化方法。

  8、如果这个Bean关联了BeanPostProcessor接口，将会调用postProcessAfterInitialization(Object obj, String s)方法、；

  注：以上工作完成以后就可以应用这个Bean了，那这个Bean是一个Singleton的，所以一般情况下我们调用同一个id的Bean会是在内容地址相同的实例，当然在Spring配置文件中也可以配置非Singleton，这里我们不做赘述。

  9、当Bean不再需要时，会经过清理阶段，如果Bean实现了DisposableBean这个接口，会调用那个其实现的destroy()方法；

  10、最后，如果这个Bean的Spring配置中配置了destroy-method属性，会自动调用其配置的销毁方法。



### 98.spring 事务实现方式有哪些？

1.编程式事务：在代码中硬编码（不推荐使用）。

2.声明式事务：在配置文件中配置（推荐使用），分为基于XML的声明式事务和基于注解的声明式事务。



### 99.说一下 spring 的事务隔离？



### ApplicationContext和BeanFactory的区别

- ApplicationContext
  - 创建容器时，创建对象采用的策略是立即加载的方式，只要一读取配置文件，马上就创建配置文件中配置的对象
  - 适用于单例模式
- BeanFactory在创建容器时
  - 采用的是延时加载的策略，什么时候根据id获取对象了，什么时候才真正的创建对象
  - 适用于多例对象



### 说一下 spring mvc 运行流程？

- MVC是一种设计模式，Spring MVC是一款很优秀的MVC框架。Spring MVC可以帮助我们进行更简洁的Web层的开发，并且它天生与Spring框架集成。Spring MVC下我们一般把后端项目分为Service层（处理业务）、Dao层（数据库操作）、Entity层（实体类）、Controller层（控制层，返回数据给前台页面）。
- 简单原理![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105112509.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

- 运行流程
  - 1.客户端（浏览器）发送请求，直接请求到DispatcherServlet。
  - 2.DispatcherServlet根据请求信息调用HandlerMapping，解析请求对应的Handler。
  - 3.解析到对应的Handler（也就是我们平常说的Controller控制器）
  - 4.HandlerAdapter会根据Handler来调用真正的处理器来处理请求和执行相对应的业务逻辑。
  - 5.处理器处理完业务后，会返回一个ModelAndView对象，Model是返回的数据对象，View是逻辑上的View。
  - 6.ViewResolver会根据逻辑View去查找实际的View。
  - 7.DispatcherServlet把返回的Model传给View（视图渲染）。
  - 8.把View返回给请求者（浏览器）

- ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105124405.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



### spring mvc 有哪些组件？

（1）前端控制器 DispatcherServlet（不需要程序员开发）

作用：接收请求、响应结果，相当于转发器，有了DispatcherServlet 就减少了其它组件之间的耦合度。

（2）处理器映射器HandlerMapping（不需要程序员开发）

作用：根据请求的URL来查找Handler

（3）处理器适配器HandlerAdapter

注意：在编写Handler的时候要按照HandlerAdapter要求的规则去编写，这样适配器HandlerAdapter才可以正确的去执行Handler。

（4）处理器Handler（需要程序员开发）

（5）视图解析器 ViewResolver（不需要程序员开发）

作用：进行视图的解析，根据视图逻辑名解析成真正的视图（view）

（6）视图View（需要程序员开发jsp）

View是一个接口， 它的实现类支持不同的视图类型（jsp，freemarker，pdf等等）



### 注解原理是什么

注解本质是一个继承了Annotation的特殊接口，其具体实现类是Java运行时生成的动态代理类。我们通过反射获取注解时，返回的是Java运行时生成的动态代理对象。通过代理对象调用自定义注解的方法，会最终调用AnnotationInvocationHandler的invoke方法。该方法会从memberValues这个Map中索引出对应的值。而memberValues的来源是Java常量池。



### Spring MVC 常用注解

- @RequestMapping：用于处理请求 url 映射的注解，可用于类或方法上。用于类上，则表示类中的所有响应请求的方法都是以该地址作为父路径。
- @RequestBody：注解实现接收http请求的json数据，将json转换为java对象。
- @ResponseBody：注解实现将conreoller方法返回对象转化为json对象响应给客户。
- @RestController注解相当于@ResponseBody ＋ @Controller,表示是表现层,除此之外，一般不用别的注解代替。



### @PathVariable和@RequestParam的区别

- 请求路径上有个id的变量值，可以通过@PathVariable来获取 @RequestMapping(value = “/page/{id}”, method = RequestMethod.GET)
- @RequestParam用来获得静态的URL请求入参 spring注解时action里用到。




# **十一、Spring Boot/Spring Cloud**

104.什么是 spring boot？



### Spring Boot启动原理

使用@SpringBootApplication注解，并在main方法里调用SpirngApplication.run()方法

@SpringBootApplication其实是一个组合注解，他包括三个注解

- @SpringBootConfiguration，再往里面其实还是使用的@Configuration注解，他表示使用java代码的方式来进行配置文件的编写，标识这个类可以成为Spring IOC中Bean对象的来源，一般会跟@Bean注解一起使用
- @EnableAutoConfiguration，借助@Import的支持（@Import(AutoConfigurationImportSelector.class)），收集和注册特定场景相关的bean定义（将所有符合条件的Bean加载到IOC容器中）。@EnableAutoConfiguration会根据类路径中的jar依赖为项目进行自动配置，如：添加了spring-boot-starter-web依赖，会自动添加Tomcat和Spring MVC的依赖，Spring Boot会对Tomcat和Spring MVC进行自动配置
- @ComponentScan，主要是指定自动扫描的包，指定把哪些包里的Bean给加载到Spring容器中

### 为什么要用 spring boot？

Spring Boot 主要有如下优点：

容易上手，提升开发效率，为 Spring 开发提供一个更快、更广泛的入门体验。
开箱即用，远离繁琐的配置。
提供了一系列大型项目通用的非业务性功能，例如：内嵌服务器、安全管理、运行数据监控、运行状况检查和外部化配置等。
没有代码生成，也不需要XML配置。
避免大量的 Maven 导入和各种版本冲突。

### spring boot 核心配置文件是什么？

- Spring Boot 的核心配置文件是 `application 和 bootstrap` 配置文件。

- application 配置文件这个容易理解，主要用于 Spring Boot 项目的自动化配置
- bootstrap 配置文件有以下几个应用场景。
  - 使用SpringCloudConfig配置中心时，这时需要在 bootstrap 配置文件中添加连接到配置中心的配置属性来加载外部配置中心的配置信息；
  - 一些固定的不能被覆盖的属性；
  - 一些加密/解密的场景；



107.spring boot 配置文件有哪几种类型？它们有什么区别？

108.spring boot 有哪些方式可以实现热部署？

109.jpa 和 hibernate 有什么区别？

110.什么是 spring cloud？

111.spring cloud 断路器的作用是什么？

### spring cloud 的核心组件有哪些？

- 服务发现——Netflix Eureka

- 客服端负载均衡——Netflix Ribbon

- 断路器——Netflix Hystrix

- 服务网关——Netflix Zuul

- 分布式配置——Spring Cloud Config



# **十二、Hibernate**

113.为什么要使用 hibernate？

114.什么是 ORM 框架？

115.hibernate 中如何在控制台查看打印的 sql 语句？

116.hibernate 有几种查询方式？

117.hibernate 实体类可以被定义为 final 吗？

118.在 hibernate 中使用 Integer 和 int 做映射有什么区别？

119.hibernate 是如何工作的？

120.get()和 load()的区别？

121.说一下 hibernate 的缓存机制？

122.hibernate 对象有哪些状态？

123.在 hibernate 中 getCurrentSession 和 openSession 的区别是什么？

124.hibernate 实体类必须要有无参构造函数吗？为什么？

# **十三、Mybatis**

### mybatis 中 #{}和 ${}的区别是什么？

-  \#{}是**预编译处理**，${}是字符串替换。

（1）mybatis在处理#{}时，会将sql中的#{}替换为?号，调用PreparedStatement的set方法来赋值。

（2）mybatis在处理${}时，就是把${}替换成变量的值。

（3）使用#{}可以有效的防止SQL注入，提高系统安全性。原因在于：预编译机制。**预编译完成之后，SQL的结构已经固定，即便用户输入非法参数，也不会对SQL的结构产生影响，从而避免了潜在的安全风险。**

（4）预编译是提前对SQL语句进行预编译，而其后注入的参数将不会再进行SQL编译。我们知道，SQL注入是发生在编译的过程中，因为恶意注入了某些特殊字符，最后被编译成了恶意的执行操作。而预编译机制则可以很好的防止SQL注入



### mybatis 有几种分页方式？

- 数组分页

  原理：进行数据库查询操作时，获取到数据库中满足条件的记录，保存在对应的List集合中，通过List.subList方法<!--其中subList(0, 5)取得的是下标为0到4的元素,不包含下标为5的元素-->，截取到满足条件的所有记录。

- SQL分页

  ```sql
  select * from student limit #{currIndex} , #{pageSize}
  ```

- 拦截器分页

  自定义拦截器实现了拦截所有以ByPage结尾的查询语句，并且利用获取到的分页相关参数统一在sql语句后面加上limit分页的相关语句

- RowBounds实现分页

  通过RowBounds实现分页和通过数组方式分页原理差不多，都是一次获取所有符合条件的数据，然后在内存中对大数据进行操作，实现分页效果。只是数组分页需要我们自己去实现分页逻辑，这里更加简化而已



128.mybatis 逻辑分页和物理分页的区别是什么？

129.mybatis 是否支持延迟加载？延迟加载的原理是什么？

### 说一下 mybatis 的一级缓存和二级缓存？

- Mybatis的一级缓存是指Session缓存。一级缓存的作用域默认是一个SqlSession。Mybatis默认开启一级缓存。
  也就是在同一个SqlSession中，执行相同的查询SQL，第一次会去数据库进行查询，并写到缓存中；
  第二次以后是直接去缓存中取。
  当执行SQL查询中间发生了增删改的操作，MyBatis会把SqlSession的缓存清空。

  一级缓存的范围有SESSION和STATEMENT两种，默认是SESSION，如果不想使用一级缓存，可以把一级缓存的范围指定为STATEMENT，这样每次执行完一个Mapper中的语句后都会将一级缓存清除。

- Mybatis的二级缓存是指mapper映射文件。二级缓存的作用域是同一个namespace下的mapper映射文件内容，多个SqlSession共享。Mybatis需要手动设置启动二级缓存。

  二级缓存是默认启用的(要生效需要对每个Mapper进行配置)，如想取消，则可以通过Mybatis配置文件中的元素下的子元素来指定cacheEnabled为false。


### 131.mybatis 和 hibernate 的区别有哪些？

- **1 开发方面**

      在项目开发过程当中，就速度而言：

  - hibernate开发中，sql语句已经被封装，直接可以使用，加快系统开发；

  - Mybatis 属于半自动化，sql需要手工完成，稍微繁琐；

      但是，凡事都不是绝对的，如果对于庞大复杂的系统项目来说，发杂语句较多，选择hibernate 就不是一个好  方案。

- **2 sql优化方面**
  - Hibernate 自动生成sql,有些语句较为繁琐，会多消耗一些性能；
  - Mybatis 手动编写sql，可以避免不需要的查询，提高系统性能；
  - Hibernate的查询会将表中的所有字段查询出来，这一点会有性能消耗。Hibernate也可以自己写SQL来指定需要查询的字段，但这样就破坏了Hibernate开发的简洁性。而Mybatis的SQL是手动编写的，所以可以按需求指定查询的字段。Hibernate HQL语句的调优需要将SQL打印出来，而Hibernate的SQL被很多人嫌弃因为太丑了。MyBatis的SQL是自己手动写的所以调整方便。但Hibernate具有自己的日志统计。Mybatis本身不带日志统计，使用Log4j进行日志记录


132.mybatis 有哪些执行器（Executor）？

133.mybatis 分页插件的实现原理是什么？

134.mybatis 如何编写一个自定义插件？

# **十四、RabbitMQ**

### rabbitmq 的使用场景有哪些？

- **异步处理**

  场景说明：用户注册后，需要发注册邮件和注册短信,传统的做法有两种1.串行的方式;2.并行的方式

  - 串行方式:将注册信息写入数据库后,发送注册邮件,再发送注册短信,以上三个任务全部完成后才返回给客户端。 这有一个问题是,邮件,短信并不是必须的,它只是一个通知,而这种做法让客户端等待没有必要等待的东西.
  - 并行方式:将注册信息写入数据库后,发送邮件的同时,发送短信,以上三个任务完成后,返回给客户端,并行的方式能提高处理的时间。

- **应用解耦**

  场景：双11是购物狂节,用户下单后,订单系统需要通知库存系统,传统的做法就是订单系统调用库存系统的接口

  - 当库存系统出现故障时,订单就会失败
  - 订单系统:用户下单后,订单系统完成持久化处理,将消息写入消息队列,返回用户订单下单成功。
  - 库存系统:订阅下单的消息,获取下单消息,进行库操作。
    就算库存系统出现故障,消息队列也能保证消息的可靠投递,不会导致消息丢失

- 流量削峰

  场景:秒杀活动，一般会因为流量过大，导致应用挂掉,为了解决这个问题，一般在应用前端加入消息队列。

  - 1.可以控制活动人数，超过此一定阀值的订单直接丢弃(我为什么秒杀一次都没有成功过呢^^)
    2.可以缓解短时间的高流量压垮应用(应用程序按自己的最大处理能力获取订单)
  - 1.用户的请求,服务器收到之后,首先写入消息队列,加入消息队列长度超过最大值,则直接抛弃用户请求或跳转到错误页面.
    2.秒杀业务根据消息队列中的请求信息，再做后续处理.



136.rabbitmq 有哪些重要的角色？

137.rabbitmq 有哪些重要的组件？

138.rabbitmq 中 vhost 的作用是什么？

139.rabbitmq 的消息是怎么发送的？

140.rabbitmq 怎么保证消息的稳定性？



### rabbitmq 怎么避免消息丢失？

为了保证数据不被丢失,RabbitMQ支持消息确认机制,为了保证数据能被正确处理而不仅仅是被Consumer收到,那么我们不能采用no-ack，而应该是在处理完数据之后发送ack.
在处理完数据之后发送ack,就是告诉RabbitMQ数据已经被接收,处理完成,RabbitMQ可以安全的删除它了.
如果Consumer退出了但是没有发送ack,那么RabbitMQ就会把这个Message发送到下一个Consumer，这样就保证在Consumer异常退出情况下数据也不会丢失.
RabbitMQ它没有用到超时机制.RabbitMQ仅仅通过Consumer的连接中断来确认该Message并没有正确处理，也就是说RabbitMQ给了Consumer足够长的时间做数据处理。
如果忘记ack,那么当Consumer退出时,Mesage会重新分发,然后RabbitMQ会占用越来越多的内存.



142.要保证消息持久化成功的条件有哪些？

143.rabbitmq 持久化有什么缺点？

144.rabbitmq 有几种广播类型？

145.rabbitmq 怎么实现延迟消息队列？

146.rabbitmq 集群有什么用？

147.rabbitmq 节点的类型有哪些？

148.rabbitmq 集群搭建需要注意哪些问题？

149.rabbitmq 每个节点是其他节点的完整拷贝吗？为什么？

150.rabbitmq 集群中唯一一个磁盘节点崩溃了会发生什么情况？

151.rabbitmq 对集群节点停止顺序有要求吗？

# **十五、Kafka**

152.kafka 可以脱离 zookeeper 单独使用吗？为什么？

153.kafka 有几种数据保留的策略？

154.kafka 同时设置了 7 天和 10G 清除数据，到第五天的时候消息达到了 10G，这个时候 kafka 将如何处理？

155.什么情况会导致 kafka 运行变慢？

156.使用 kafka 集群需要注意什么？

# **十六、Zookeeper**

157.zookeeper 是什么？

158.zookeeper 都有哪些功能？

159.zookeeper 有几种部署模式？

160.zookeeper 怎么保证主从节点的状态同步？

161.集群中为什么要有主节点？

162.集群中有 3 台服务器，其中一个节点宕机，这个时候 zookeeper 还可以使用吗？

163.说一下 zookeeper 的通知机制？

# **十七、MySql**

### 数据库的三范式是什么？

- 第一范式：1NF是对属性的原子性约束，要求字段具有原子性，不可再分解；(只要是关系型数据库都满足1NF)
- 第二范式：2NF是在满足第一范式的前提下，非主键字段不能出现部分依赖主键；解决：消除复合主键就可避免出现部分以来，可增加单列关键字。
- 第三范式：3NF是在满足第二范式的前提下，非主键字段不能出现传递依赖，比如某个字段a依赖于主键，而一些字段依赖字段a，这就是传递依赖。解决：将一个实体信息的数据放在一个表内实现。



165.一张自增表里面总共有 7 条数据，删除了最后 2 条数据，重启 mysql 数据库，又插入了一条数据，此时 id 是几？

166.如何获取当前数据库版本？



### 说一下 ACID 是什么？

- 1.Atomicity 原子性：指的是整个事务是一个独立的单元，要么操作成功，要么操作不成功
- 2.Consistency 一致性：事务必须要保持和系统处于一致的状态（如果不一致会导致系统其它的方出现bug）
- 3.Isolation 隔离性 事务是并发控制机制，他们的交错也需要一致性，隔离隐藏，一般通过悲观或者乐观锁实现
- 4.Durability 耐久性 一个成功的事务将永久性地改变系统的状态，所以在它结束之前，所有导致状态的变化都



168.char 和 varchar 的区别是什么？

169.float 和 double 的区别是什么？

170.mysql 的内连接、左连接、右连接有什么区别？

171.mysql 索引是怎么实现的？

172.怎么验证 mysql 的索引是否满足需求？



### 173.说一下数据库的事务隔离？

有4种隔离级别，以AB事务来模拟

读未提交：A写入数据的时候，B不允许写入，但是可以读，会造成B查看了A尚未提交的数据。

读提交：A读取数据的时候允许B读取，但是A在写入且没有提交的时候禁止B查看。

可重复读：AB会拿到同样的数据

序列化：如同字面意思，AB不能同时干活，需要按照顺序来执行，但是加大了开销



### 174.说一下 mysql 常用的引擎？

InnoDB：支持事务处理，支持外键，支持崩溃修复能力和并发控制。如果需要对事务的完整性要求比较高（比如银行），要求实现并发控制（比如售票），那选择InnoDB有很大的优势。如果需要频繁的更新、删除操作的数据库，也可以选择InnoDB，因为支持事务的提交（commit）和回滚（rollback）。
MyISAM：插入数据快，空间和内存使用比较低。如果表主要是用于插入新记录和读出记录，那么选择MyISAM能实现处理高效率。如果应用的完整性、并发性要求比较低，也可以使用。
MEMORY：所有的数据都在内存中，数据的处理速度快，但是安全性不高。如果需要很快的读写速度，对数据的安全性要求较低，可以选择MEMOEY。它对表的大小有要求，不能建立太大的表。所以，这类数据库只使用在相对较小的数据库表。



### 说一下 mysql 的行锁和表锁？

- 表级锁：开销小，加锁快，不会出现死锁。锁定粒度大，发生锁冲突的概率最高，并发量最低
- 行级锁：开销大，加锁慢，会出现死锁。锁力度小，发生锁冲突的概率小，并发度最高
-

### 176.说一下乐观锁和悲观锁？

乐观锁：对于每次请求，都会做最乐观的打算，认为该请求不会修改数据，但是在更新的时候会去判断在这个期间，有没有别的请求修改了这个值，CAS使用的就是这种思想，每次都将期望值和主物理内存中的值对比，如果相同才修改为更新值。

悲观锁：对于每次请求，都会做最悲观的打算，认为该请求会修改数据，每次请求都会加锁，synchroniezd和Lock锁都使用的这种思想，每次都将整个方法或者代码块锁住。



### 共享锁和排他锁

对某一资源加共享锁，自身可以读该资源，其他人也可以读该资源（也可以再继续加共享锁，即 共享锁可多个共存），但无法修改。要想修改就必须等所有共享锁都释放完之后



177.mysql 问题排查都有哪些手段？

178.如何做 mysql 的性能优化？

# **十八、Redis**

### 缓存的三大问题

#### 缓存穿透

缓存穿透是指缓存和数据库中都没有的数据，而用户不断发起请求，如发起为id为“-1”的数据或id为特别大不存在的数据。这时的用户很可能是攻击者，攻击会导致数据库压力过大

- 接口层增加校验，如用户鉴权校验，id做基础校验，id<=0的直接拦截；
- 从缓存取不到的数据，在数据库中也没有取到，这时也可以将key-value对写为key-null，缓存有效时间可以设置短点，如30秒（设置太长会导致正常情况也没法使用）。这样可以防止攻击用户反复用同一个id暴力攻击
- 采用布隆过滤器，使用一个足够大的bitmap，用于存储可能访问的key，不存在的key直接被过滤



#### 缓存击穿

一个存在的key，在缓存过期的一刻，同时有大量的请求，这些请求都会击穿到DB，造成瞬时DB请求量大、压力骤增

- 设置热点数据永远不过期
- 加互斥锁

#### 缓存雪崩

179.redis 是什么？都有哪些使用场景？

180.redis 有哪些功能？

181.redis 和 memecache 有什么区别？

182.redis 为什么是单线程的？

183.什么是缓存穿透？怎么解决？

184.redis 支持的数据类型有哪些？

185.redis 支持的 java 客户端都有哪些？

186.jedis 和 redisson 有哪些区别？

187.怎么保证缓存和数据库数据的一致性？

188.redis 持久化有几种方式？

189.redis 怎么实现分布式锁？

190.redis 分布式锁有什么缺陷？

191.redis 如何做内存优化？

192.redis 淘汰策略有哪些？

193.redis 常见的性能问题有哪些？该如何解决？

# **十九、JVM**

### 说一下 jvm 的主要组成部分？及其作用？

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105428455.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

- 1.类加载器（Class Loader）：加载类文件到内存。Class loader只管加载，只要符合文件结构就加载，至于能否运行，它不负责，那是有Exectution Engine 负责的。

- 2.执行引擎（Execution Engine）：也叫解释器，负责解释命令，交由操作系统执行。

- 3.本地库接口（Native Interface）：本地接口的作用是融合不同的语言为java所用

- 4.运行时数据区（Runtime Data Area）：



195.说一下 jvm 运行时数据区？

196.说一下堆栈的区别？

198.什么是双亲委派模型？

### 说一下类加载的执行过程？

- 一个Java文件从编码完成到最终执行，一般主要包括两个过程
  - 编译：即把我们写好的java文件，通过javac命令编译成字节码，也就是我们常说的.class文件
  - 运行：则是把编译声称的.class文件交给Java虚拟机(JVM)执行
- 类加载过程即是指JVM虚拟机把.class文件中类信息加载进内存，并进行解析生成对应的class对象的过程

- 具体过程如下：
  - 1. 加载：将.class文件加载进内存，在堆中生成一个Class对象来保存这个类，作为访问该对象的入口。
    2. 连接：连接分为三个步骤
       1. 验证：确保加载的类信息符合JVM规范，没有安全方面的问题
       2. 准备：正式为静态变量分配内存空间
       3. 解析：虚拟机常量池内的符号引用改为地址引用的过程，也就是为变量绑定对应的内存地址
    3. 初始化：执行类构造器的方法，对静态变量和静态代码块进行复制，也就是说其实在连接时只是为这些变量分配了内存空间，真正的赋值是在初始化的时候

### **类加载的三种方式**

- 命令行启动应用时由JVM初始化加载
- 通过Class.forName() 方式动态加载
- 通过ClassLoder.loadClass() 方法动态加载）



### 怎么判断对象是否可以被回收？

- 引用计数法(java中没用，因为，没办法解决循环引用：A引用B，B也引用A，但是没有其他引用去引用A和B，这时AB都是垃圾，但是引用计数法无法判断)。
- 可达性分析算法：通过GC Roots为起始点向下搜索，说白了就是通过你已知的活对象，去找这对象里的引用，再找引用对象里的引用，一直这样下去，找的到的就是活的。
- 那么哪些对象可以作为GC Roots呢：
  - 1虚拟机栈中引用的对象。
  - 2方法区静态属性引用的对象。
  - 3方法区中常量引用的对象。
  - 4本地方法栈中JNI(一般说的是Native方法)引用的对象）



201.java 中都有哪些引用类型？

202.说一下 jvm 有哪些垃圾回收算法？

203.说一下 jvm 有哪些垃圾回收器？

204.详细介绍一下 CMS 垃圾回收器？

205.新生代垃圾回收器和老生代垃圾回收器都有哪些？有什么区别？

206.简述分代垃圾回收器是怎么工作的？

207.说一下 jvm 调优的工具？

208.常用的 jvm 调优的参数都有哪些？

### JVM垃圾回收时如何确定垃圾？什么是GC Roots

- 什么是垃圾？
  - 简单来说就是内存中已经不再被使用到的空间就是垃圾
- 如何判断一个对象是否可以被回收
  - 引用计数法
    - 给对象添加一个引用计数器，每当有一个地方引用他，计数器的值加1，引用失效时，计数值减1，但是他很难解决循环引用的问题
  - 枚举根节点做可达性分析（根搜索路径，也就是GC Roots）
    - 基本思路就是通过一系列的名为“GC Root”的对象作为起始点，从这个被称为GC Root的对象开始向下搜索，如果一个对象到GC Root没有任何引用链相连时，则说明此对象不可用。也就是给定一个集合的引用作为根出发，通过引用关系遍历对象图，能被遍历到的对象就判定为存活，没有被遍历到的就判定为死亡
    - 能够作为GC Roots对象的有四种
      - 虚拟机栈中引用的对象
      - 方法区中的类静态属性引用的对象
      - 方法区中常量引用的对象
      - 本地方法栈（Native方法）中引用的对象



### 强引用/软引用/弱引用/虚引用

- 强![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105444771.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

- 软![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105454714.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



- 弱![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105505882.png)



-  虚![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105515996.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)
  可以通过判断queue里面是不是有对象来判断你的对象是不是要被回收了

- 软引用和弱引用的场景![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105526464.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



- ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105537178.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)




### 谈谈你对OOM的认识

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105546906.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



### GC垃圾回收算法

#### 复制算法

- 复制算法将可用的内存分成两份，每次使用其中一块，当这块回收之后把未回收的复制到另一块内存中，然后把使用的清除。这种算法运行简单，解决了标记-清除算法的碎片问题，但是这种算法代价过高，需要将可用内存缩小一半，对象存活率较高时，需要持续的复制工作，效率比较低。

#### 标记清除

- 该算法先标记，后清除，将所有需要回收的算法进行标记，然后清除；这种算法的缺点是：效率比较低；标记清除后会出现大量不连续的内存碎片，这些碎片太多可能会使存储大对象会触发GC回收，造成内存浪费以及时间的消耗。

#### 标记压缩

- 标记整理算法是针对复制算法在对象存活率较高时持续复制导致效率较低的缺点进行改进的，该算法是在标记-清除算法基础上，不直接清理，而是使存活对象往一端游走，然后清除一端边界以外的内存，这样既可以避免不连续空间出现，还可以避免对象存活率较高时的持续复制。这种算法适合老生代。

#### 分代收集

- 分代收集算法就是目前虚拟机使用的回收算法，它解决了标记整理不适用于老年代的问题，将内存分为各个年代，在不同年代使用不同的算法，从而使用最合适的算法，新生代存活率低，可以使用复制算法。而老年代对象存活率高，没有额外空间对它进行分配担保，所以使用标记整理算法。



### 4种主要的垃圾收集器

#### Serial（串行垃圾回收器）

- 它为单线程环境设计且只使用一个线程进行垃圾回收，会暂停所有的用户线程，所以不适合服务器环境

#### Parallel（并行垃圾回收器）

- 多个垃圾收集线程并行工作，此时用户线程是暂停的，适用于科学计算/大数据处理首台处理等弱交互环境

#### CMS（并发垃圾回收器）

- 用户线程和垃圾收集线程同时执行（不一定是并行，可能交替执行），不需要停顿用户线程，适用于对响应时间有要求的场景

#### G1

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105557793.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706105605760.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)







#### Roots

- 什么是垃圾？
  - 简单来说就是内存中已经不再被使用到的空间就是垃圾
- 如何判断一个对象是否可以被回收
  - 引用计数法
    - 给对象添加一个引用计数器，每当有一个地方引用他，计数器的值加1，引用失效时，计数值减1，但是他很难解决循环引用的问题
  - 枚举根节点做可达性分析（根搜索路径，也就是GC Roots）
    - 基本思路就是通过一系列的名为“GC Root”的对象作为起始点，从这个被称为GC Root的对象开始向下搜索，如果一个对象到GC Root没有任何引用链相连时，则说明此对象不可用。也就是给定一个集合的引用作为根出发，通过引用关系遍历对象图，能被遍历到的对象就判定为存活，没有被遍历到的就判定为死亡
    - 能够作为GC Roots对象的有四种
      - 虚拟机栈中引用的对象
      - 方法区中的类静态属性引用的对象
      - 方法区中常量引用的对象
      - 本地方法栈（Native方法）中引用的对象
