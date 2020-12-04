写在最前：此篇文章对应周阳老师的大厂面试教程，几乎包含了大厂所有JUC部分的面试题，虽然自己无缘大厂，但是这些知识也让我在面试中得到了不错的评价。需要找工作的同学可以搭配另一篇文章来使用


# JUC

java.util.concurrent的缩写

### 线程的6种状态

创建，可运行，阻塞，等待，计时等待，终结



### Lambda表达式

java1.8之后允许接口中有部分方法的实现，需要用default关键字描述方法

@FunctionalInterface 注解表示函数式接口（仅有一个抽象方法）



### 常见异常总结

ConcurrentModificationException：当方法检测到对象的并发修改，但不允许这种修改时，抛出此异常

StackOverflowError：



### 多线程案例

![C:\Users\WHB\AppData\Roaming\Typora\typora-user-images\image-20200513164544239.png](https://img-blog.csdnimg.cn/20200706101730410.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

新老技术方案

*JDK*1.5中将*Lock*接口*代替synchronized*升级为显示的锁机制

lock代替了synchronized关键字，Condition进行通信

Condition.await()代替了wait

Condition.signal()代替了notify				signal信号

### Synchronized

Synchronized关键字，同一时间只能有一个进程进入类中的Synchronized方法，相当于对象锁

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706101757176.png)


static synchronized 锁的是类（.class），锁的是类的模板



### ConcurrentModificationException异常

原因：当方法检测到对象的并发修改，但不允许这种修改时，抛出此异常

解决方案：

	1.可以使用Vector类，因为Vector中的add方法带有synchronized关键字
	
	2.Collections.synchronizedList 使用Collections工具栏把List变为线程安全
	
	3.使用JUC中的CopyOnWriteArrayList类，采用了写时复制的思想（读写分离），使用lock锁

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706101812247.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706101826809.png)



### HashSet

hashset底层是hashmap,hashset的构造方法其实就是new了一个hashmap，在执行add方法时，调用的是map的put方法，key为加入的值，value是一个默认值（PRERSEND常量）

```java
public boolean add(E e) {
    return map.put(e, PRESENT)==null;
}
```

```java
public HashSet() {
    map = new HashMap<>();
}
```

ArryList扩容为原来的一半，HashMap为原来的一倍

### 获取多线程的方式

1.继承Thread类

2.实现Runnble接口

3.实现Callable接口

### Callable接口和Runnble接口的区别

1.Callable有返回值

2.Callable会有异常

3.Callable执行的是call方法，Runnble是run方法

Callable接口的get方法一般放在最后一行



### CountDownLatch

- countDownLatch这个类使一个线程等待其他线程各自执行完毕后再执行。

  是通过一个计数器来实现的，计数器的初始值是线程的数量。每当一个线程执行完毕后，计数器的值就-1，当计数器的值为0时，表示所有线程都执行完毕，然后在闭锁上等待的线程就可以恢复工作了

  

###  CyclicBarrier

- 一个同步帮助，允许一组线程相互等待，以达到一个共同的障碍点。cyclicbarriers涉及一个固定大小的线程必须党偶尔互相等待程序是有用的。该障碍被称为循环，因为它可以在等待线程被释放后重新使用。
- CountDownLatch做减法，CyclicBarrier做加法



### Semaphore

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706101918232.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

### ReadWriteLock

读写锁



### BlockingQueue

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706101932808.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706101942966.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706101952629.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070610200212.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

### 线程池

#### 线程池的优势

线程池的工作主要是控制运行的线程数量，处理过程中将任务放入队列，然后在线程创建后启动这些任务，如果线程数量超过了最大数量，超出数量的线程排队等候，等待其他线程执行完毕，再从队列中取出任务来执行。

主要特点

- 线程复用
- 控制最大并发量
- 管理线程

#### ThreadPoolExecutor

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102015827.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

ThreadPoolExecutor是线程池的主要操作类，上图的三个分别为指定线程数，单一线程，自动扩容线程

他们底层都是调用了ThreadPoolExecutor类的构造方法来实现

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102025164.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### 七大参数

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102034174.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### 工作原理

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102043285.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102052117.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102101254.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### 一般使用哪种线程池

![](https://img-blog.csdnimg.cn/20200706102142542.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



#### 四大拒绝策略
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102158781.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



##### AbortPolicy

超过线程数会抛出异常    abort:中止计划

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102208155.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



##### CallerRunsPolicy

会将任务退回到执行人处

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102220470.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

##### DiscardOldestPolicy

抛弃等待最久的  Discard：抛弃

##### DiscardPolicy

不处理



### 函数式接口

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102231513.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

### Stream流

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102249861.png)

##### 特点

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102257806.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



### ForkJoin

分支合并框架

```java
class MyTask extends RecursiveTask<Integer>{

    private static final Integer ADJUST_VALUE = 10;

    private int begin;
    private int end;
    private int result;

    public MyTask(int begin, int end) {
        this.begin = begin;
        this.end = end;
    }

    @Override
    protected Integer compute() {
        if ((end-begin)<=ADJUST_VALUE){
            for (int i = begin; i <=end ; i++) {
                result = result+i;
            }
        }else {
            int middle = (end+begin)/2;
            MyTask task1 = new MyTask(begin,middle);
            MyTask task2 = new MyTask(middle+1,end);
            task1.fork();
            task2.fork();
            result = task1.join()+task2.join();
        }
        return result;
    }
}

public class ForkJoinDemo {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        MyTask myTask = new MyTask(0,2000);
        ForkJoinPool threadPool = new ForkJoinPool();
        ForkJoinTask<Integer> forkJoinTask = threadPool.submit(myTask);
        System.out.println(forkJoinTask.get());
        threadPool.shutdown();
    }
}
```

# JVM

### JVM体系结构
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102307530.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

灰色的是线程私有的，黄色的是共享的（存在垃圾回收）



### 类加载器ClassLoader

------

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102316981.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102326688.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

JAVA自带的使用Bootstrap加载器

自己编写的类使用AppClassLoader加载器





#### 双亲委派机制

我爸是李刚，有事找我爹

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102347566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### 沙箱安全

防止自己写的代码污染JDK中的包



### Native

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102358610.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102407943.png)



native是一个关键字

含有native关键字的方法只有声明，没有实现，因为他是调用的C语言







### PC寄存器

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102416918.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

记录了方法之间的调用和执行情况，用来存储指向下一条指令的地址，也就是即将要执行的指令代码，他是当前线程所执行的字节码的行号显示器



### 方法区

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102427377.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102435630.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



------

### 栈

- 栈管运行，堆管存储

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102444324.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

8种基础类型，实例方法，对象的引用变量存在栈中

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102453114.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102504467.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



#### 堆 栈 方法区的交互关系

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070610251285.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

### 堆 heap

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070610252172.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102529836.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102537738.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102547737.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070610255776.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102604595.png)

### 堆参数调优

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102613724.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### JDL1.7演示

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102622521.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### JDK1.8演示
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102631256.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)



### GC是什么

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102644489.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)
### Minor GC和Full GC的区别

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070610265256.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

### 4大算法

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102701349.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)
#### 1.引用计数法

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070610270939.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### 2.复制算法

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102717383.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102725888.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070610273394.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### 3.标记清楚

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102740575.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102749342.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102756322.png)



#### 4.标记压缩

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102807562.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### 总结

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070610281569.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102824225.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### 面试题
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102836478.png)

### JMM

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102844934.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)


#### 3.标记清楚

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706103050675.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706103104331.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706103114763.png)



#### 4.标记压缩

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706103038682.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### 总结

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706103015370.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706103026710.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

#### 面试题

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706103003268.png)

### JMM

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102948376.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706102909976.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQzMTc2Ng==,size_16,color_FFFFFF,t_70)