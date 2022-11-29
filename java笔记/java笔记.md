# Java学习笔记

（基于学过c&cpp）

## JavaSE

> 主要参考资料
>
> 1. 尚硅谷Java入门视频教程:30天搞定java(bilibili)

#### 源文件编译

一个源文件中最多只能有一个public类。如果源文件有public类，则文件名必须按该类名命名。

命令行编译运行：

```plaintext
//法一：分步编译运行
//编译生成.class文件
javac xxx.java
//运行.class文件
java xxx

//法二：一步直接编译运行(java9)
java xxx.java

//法三：使用jshell命令编写运行代码块(java9)
```

#### 文档注释

- 格式：/**……*/常见：
  ```java
  /**  
  *@author 指定java程序的作者  
  *@version 指定源文件的版本  
  *其他javadoc 标签  
  */  
  ```
- Public和protected的注释内容可以被JDK提供的工具 javadoc 所解析，生成一套以网页文件形式体现的该程序的说明文档。
- 单行多行注释同c++

#### 命名规范

- 包名：字母都小写
- 类名、接口名：所有单词的首字母大写
- 变量名、方法名：第一个单词首字母小写，第二个单词开始每个单词首字母大写
- 常量名：字母都大写，多单词时用下划线

#### 输入输出

##### 屏幕输出

- System.out.print();输出
- System.out.println();输出并换行

##### 键盘输入

- ```java
  import java.util.Scanner;   
  Scanner 【对象名】=new Scanner(System.in);  
  【数据类型】【接收变量】=【对象名】.next【首字母大写的类型名】();
  //...
  【对象名】.close();  
  ```
- next()读取字符串（直到空白字符为止），nextLine()读取一行字符串
- 对char没有提供方法

#### 数据类型

- 基本数据类型：
  - byte字节整形 范围-128~127
  - char 2字节（Java中字符用Unicode编码（\uXXXX））
  - boolean布尔类型，不可以使用0或非 0 的整数替代false和true
  - java的整型常量默认为 int 型，浮点型默认为double型，故声明long须在字面量后加‘l’或‘L’，声明float须在字面量后加‘f’或‘F’
  - 数字字面量的数位之间可增加下划线来提高可读性
- 引用数据类型：
  1. 类
  2. 接口
  3. 数组
- 注意事项
  - byte,short,char之间不会相互转换，在计算时首先转换为int类型。
  - String与其他类型+运算效果是连接，结果类型转为String
  - 创建引用类型时，runtime会为其分配两个空间，一块空间分配在堆上，存储引用类型本身的数据，另一个块空间分配在栈上，存储对堆上数据的引用，实际上存储的堆上的内存地址。故在赋值操作时实际上为指针传递。

#### 语句块

- switch(表达式)中表达式的值必须是下述几种类型之一：byte，short，char，int，枚举 (jdk 5.0)，String (jdk 7.0)； case子句中的值必须是常量；
- break;continue;可带标签（可一次性跳出多重循环），其后不能声明执行语句

#### 数组

- 声明：`【数据类型】 【变量名】[] 或【数据类型】[] 【变量名】;`声明时不能指定其长度。
- 定义/创建实例：`new 【数据类型】[【数组长度】]`
- 常用功能：a.length 指明数组a的长度(元素个数)；java.util.Arrays工具类中提供的一系列静态方法；
- 多维数组可看作树状结构，不必都是规则矩阵形式，但须初始化最高层长度

#### 类

- 成员(field&method)的访问权限类型通过前缀添加
  1. Private：可被自身所在的类成员访问
  2. 默认：可被同一包中的所有类访问
  3. Protected：可被同一包中的所有类，以及不同包中的子类访问
  4. Public：可被同一工程/项目中的所有类访问
- 属性可初始化；
- Java里所有方法必须定义在类里；不可以在方法内部定义方法。
- 构造器：不能被static、final、synchronized、abstract、native修饰，不能有return语句返回值， 默认构造器的修饰符与所属类的修饰符一致。
- 创建对象：`【类名】 【对象名】 = new 【类名】();`
- 对象通过点运算符调用成员属性或方法；
- 匿名对象常做方法实参
- Java里方法的参数传递方式只有一种：值传递
- 使用this访问属性和方法时，如果在本类中未找到，会从父类中查找。
- this(…);写在首行用于构造器调用其他构造器
- java一个源文件只能有一个public类：表示每个编译单元都只能有唯一的同名的公共接口
- 代码块成员：常用于对类或对象进行初始化
  - 类中非静态代码块也称构造代码块
  - 静态代码块不可以调用非静态的属性和方法
  - 静态代码块的执行要先于非静态代码块
  - 静态代码块随着类的加载而执行；非静态代码块每次创建对象（调用构造器）的时候都会先执行一次。
  - 成员变量的显式初始化和代码块中的初始化，按照写的先后顺序执行

#### 可变个数参数Varargs(jdk5.0+）

- 允许直接定义能接受可变个数实参的形参，等效于传入数组
- 同一个方法只能在形参列表末位声明一个可变个数形参
- 格式：`【数据类型】…【形参名】`

#### 包

- `package 【顶层包名】.【子包名】;` 常作为第一条语句，标识其后代码所属的包名
- 包通常使用所在公司域名的倒置
- Jdk：
  1. java.lang----包含核心类如String、Math、Integer、 System和Thread
  2. java.net----包含执行与网络相关的操作的类和接口。
  3. java.io ----包含能提供多种输入/输出功能的类。
  4. java.util----包含一些实用工具类，如定义系统特性、接口的集合框架类、使用与日期日历相关的函数。
  5. java.text----包含了一些java格式化相关的类
  6. java.sql----包含了java进行JDBC数据库编程的相关类/接口
  7. java.awt----包含了构成抽象窗口工具集（abstract window toolkits）的多个类，这些类被用来构建和管理应用程序的图形用户界面(GUI)。
- 导包：
  - 格式：`import 【包名】.【类名】;`
  - 类名可用*代替，表示导入其下所有类（不包括子包）
  - java.lang包或当前包下可省略
  - 若类重名，只能导入一个，其他需写全名
  - import 后缀static：调用指定类或接口下的静态的属性或方法

#### 类继承

- 格式：`【subclass/子类/派生类】extends【superclass/父类/超类/基类】`
- Java只支持单继承（单个父类）和多层继承，不允许多重继承
- 所有类都直接或间接继承于java.lang.Object类
- 方法重写override：
  1. 子类重写的方法的返回值类型不能大于父类被重写的方法的返回值类型
  2. 子类重写的方法使用的访问权限不能小于父类被重写的方法的访问权限
  3. 子类方法抛出的异常不能大于父类被重写方法的异常
- 子父类中同名属性可以共存
- `super:`访问父类定义的属性、方法、构造器（可层层向上追溯）

#### 多态

- Java引用变量有两个类型：编译时类型和运行时类型。编译时类型由声明该变量时使用的类型决定，运行时类型由实际赋给该变量的对象决定。
- `x instanceof A`检验x本质上是否为类A（的子类）的对象，返回值为boolean型。（常用于判断是否需要进行父子类之间的强制类型转换）

#### java.lang.Object类

- equals方法默认相当于==（比较指针），要比较指向内容的话需重写
- toString方法默认返回类名@哈希值，要返回内容需重写（输出语句中会自动调用该方法，字符数组除外，字符数组直接拼接输出）

* wait() 同步监视器调用，阻塞当前线程并释放锁
* notify() notifyAll() 同步监视器调用，唤醒阻塞的线程

#### 包装类

- 针对八种基本数据类型定义相应的引用类型
- Jdk5.0+实现了自动装箱自动拆箱，直接=赋值即可
- Integer的内部类IntegerCache中有一个存有-128~127的整型数组，在此范围内的对象初始化都不用再new，而是直接引用该数组
- 包装类对象可强制转换成对应的数据类型
- 易错题：
  ```java
  Object o1 =true? new Integer(1): new Double(2.0);  
  System. out. println(o1);//输出1.0
  ```
- 基本数据类型/包装类转换为String：法1：连接运算符+法2：调用String类的valueOf方法
- String转换为基本数据类型/包装类：调用包装类的【parse包装类】方法

#### 类之间的关系

1. 依赖Dependency：中一般指由局部变量、函数参数、返回值建立的对于其他对象的调用关系。
2. 关联Association：一种引用关系，通常使用类的属性表达（同一层次，有关联）
3. 聚合Aggregation：has-a 关系，通常使用类的属性表达（不同层次，部分与整体）
4. 组合Composite：contains-a ，关系一种更强的关联包含关系，通常使用类的属性表达，组合类负责被组合类的生命周期
5. 继承/泛化Generalization

#### 设计模式

在大量的实践中总结和理论化之后优选的代码结构、编程风格、以及解决问题的思考方式。

- 单例 (Singleton)模式
  - 一个类只存在一个唯一的对象实例（构造器设为private），这个实例在类中创建为静态的，该类提供一个取得其对象实例的静态方法
  - 实现方式分为 饿汉式(静态对象默认初始化为一个实例)、懒汉式（当调用get方法时才判断需不需要创建实例）
  - 常用于：网站的计数器、应用程序的日志应用、数据库连接池、读取配置文件的类、Application、Windows的Task Manager (任务管理器)和Recycle Bin (回收站)
- 代理模式：代理类内含了被代理类的对象并实现了被代理类实现的接口，使得代理类和被代理类之间通过接口交互，被代理类和外界之间通过被代理类交互，使得被代理类不被直接暴露。
- 工厂模式：实现了创建者与调用者的分离，即将创建对象的具体过程屏蔽隔离起来，达到提高灵活性的目的。

#### final

- 标记的类不能被继承
- 标记的方法不能被子类重写
- 标记的变量为常量，不能被默认初始化

#### 接口

是抽象方法和常量值定义的集合，本质是一种特殊的抽象类

- 所有成员变量都默认是由public static final修饰的（即常量）。
- 所有成员方法都默认是由public abstract修饰的（即抽象方法）。
- 没有构造器。
- 接口允许多继承接口
- 一个类可以实现多个接口 `implements 【接口1】,【接口2】…`
- JDK7.0+可包含静态方法（public static）和默认方法（public default…若与父类方法同名默认调父类，但可通过【接口】.super.【方法名】调用）
- 接口也可以作实现多态的形参
- 对于实现类、抽象类和接口，优先使用接口，其次抽象类。

#### 内部类

- 编译以后生成OuterClass$InnerClass.class字节码文件
- 访问：通过点运算符
- 若在局部内部类中调用了所在方法的局部变量，要求该变量为final

#### 异常

- 异常throwable，分为Error和Exception，后者又分为编译时/受检异常（必须处置即捕获或声明否则编译错误）和运行时/非受检异常RuntimeException（可以不处理，Java自己能捕获并编译通过，只是运行时可能会发生异常使得程序运行终止）
- 理解区分上述二者？
- 开发中，通常不对运行时异常编写异常的处理而是修改代码，但必须对编译时异常考虑异常的处理，
- Java程序的执行过程中如出现异常，会自动或程序员手动生成并抛出一个异常类对象，一旦抛出其后代码不再执行
- 手动生成并抛出异常对象：throw new【异常类型】(【自定义异常信息】)
- 处理方式一：try-catch-finally
  - 格式：
    ```java
    try{【包含可能抛出异常的代码和如果异常应该跳过的代码】}
    catch(【异常类型1】【变量1】){【异常处理代码】} 
    catch(【异常类型2】【变量2】){【异常处理代码】} 
    ……
    finally{【一定会执行的代码】}//（可选的）
    ```
  - try中一旦抛出异常则根据异常类型匹配进入catch中处理，然后跳出try-catch结构继续执行之后的代码
  - catch中常调用异常变量的getMessage方法和printStackTrace方法
  - try-catch中定义的变量生命周期在其中
  - try-catch可将编译时异常延迟到运行时
  - finally常用情况包括try-catch中有return，或catch中仍抛出异常，或需手动回收资源等，相当于提供一个统一出口
  - try-catch结构可相互嵌套
- 处理方式二：throws + 异常类型
  - 格式：方法头体前缀throws 【异常类型1】,【异常类型2】……
  - 可层层向调用者抛出异常直到被处理为止，若main仍不处理则程序终止
- 自定义异常类：
  - 继承于Exception
  - 定义类ID：static final long serialVersionUID=…;
  - 定义构造器（常包括空参的和接受异常信息的）

#### 其他

- 只有成员变量才有默认值，而局部变量必须要赋初值。
- 对于引用数据类型而言，默认初始化值为null
- 框架：
  ```java
  public class 【类名】{
      public static void main(String[] args){
      }
  }
  class 【其他类】{}
  …… 
  ```
- ++、--、+=……不会改变自身数据类型
- &与（无论左式任何右式都会运算），&&短路与；|和||同理
- `>>>` 无符号右移
- ==：基本数据类型中比较相同数据类型（可能会触发自动类型提升）的值，引用数据类型中比较地址值
- 创建匿名子类对象：`new 【父类】(){【重写的方法】};`

#### 字符串

##### String类

- 定义为final的java.lang.String类
- 可直接用双引号创建对象，储存在字符串常量池中（不会储存相同的字符串）。常量拼接结果在常量池中，涉及变量结果在堆空间。
- 内部包含一个final的字符数组value（final意味着不可变，若涉及修改则返回一个新对象）
- 常用方法
  - length
  - chartAt(int index)
  - toLowerCase()、toUpperCase()
  - trim():返回字符串的副本，忽略前后空白
  - equals(Object obj)、equalsIgnorecase(String anotherstring)
  - compareTo(String anotherstring)返回int差值
  - substring(int beginIndex,int endIndex)返回字符串的子段
  - contain(String substring)、indexOf(String substring)
  - getBytes()getChars()提取为对应的字节数组、字符数组
  - replace()
  - matches(String regex)正则匹配、split(String regex)正则切割
  - intern返回字符串的常量池地址
  - toCharArray()转换为数组

##### StringBuffer

可变的字符序列（底层由非final的字符数组存储）；线程安全但低效的；

* 创建对象时默认创建一个多余了16长度capacity的字符数组
* 扩容问题：修改后字符序列长度若超过原字符数组长度，一般将原容量x2+2，仍不足则直接将新序列长度作为容量
* 可显示指定容量初始化

##### StringBuilder(JDK1.5+)

类似于StringBuffer，但是线程不安全但高效的；

#### 多线程

* 线程基本概念属于操作系统知识，不再赘述。
* java程序支持多线程
* java线程调度策略：同优先级线程先到先服务+时间片；高优先级使用优先调度的抢占式策略
* Thread类

  * 优先级常量
    * MAX PRIORITY:10
    * MIN PRIORITY:1
    * NORM_PRIORITY:5 默认
  * 常用方法
    * 静态方法currentThread返回当前线程对象
    * getName setName
    * yield
    * join
    * 静态方法sleep
    * isAlive
    * getpriority setpriority
* 创建分线程

  * 法一：调用Thread的自定义子类（自定义一个继承于Thread的子类并重写其run方法，再在程序中实例化上述子类并调用其start方法。）
  * 法二：实现Runnable接口（自定义一个类实现Runnable接口的run方法，再在程序中将上述类对象作为参数传入Thread对象构造器中，最后调用Thread对象的start方法）
  * 法三：实现Callable接口(JDK1.5+)（自定义一个类实现Runnable接口的run方法，然后在程序中将上述类对象作为参数传入FutureTask对象构造器中，再将FutureTask对象作为参数传入Thread对象构造器中，最后调用Thread对象的start方法，另外调用FutureTask对象的get方法可获取call方法返回值）（相比run，call有返回值、返回值支持泛型且可抛出异常）
  * 法四：线程池(JDK1.5+)
    * Executors：线程池的工厂类，下列静态创建方法返回值类型为ExecutorService（实现该接口的子类如ThreadPoolExecutor）
       Executors.newCachedThreadPool()：创建一个可根据需要创建新线程的线程池
       Executors.newFixedThreadPool(n); 创建一个可重用固定线程数的线程池
       Executors.newSingleThreadExecutor() ：创建一个只有一个线程的线程池
       Executors.newScheduledThreadPool(n)：创建一个线程池，它可安排在给定延迟后运
      行命令或者定期地执行。
    * ExecutorService：线程池接口
       execute(Runnable command) ：执行（从线程池中获取线程，执行线程，并返回给线程池）
       `<T>` Future `<T>` submit(Callable `<T>` task)：执行（从线程池中获取线程，执行线程，并返回给线程池）
       shutdown() ：关闭池连接
* 线程安全问题的解决方法

  * 法一：同步代码块。`synchronized (【锁对象/同步监视器（常用this或该类）】){【需要同步的代码】}`
  * 法二：同步方法。需要同步的代码声明在一个方法中，可考虑将该方法声明为 synchronized（非静态的同步方法，同步监视器是this；静态的同步方法，同步监视器是当前类）
  * 法三：Lock锁(JDK1.5+)。使用锁对象（通常创建实现了Lock接口的ReentrantLock类的一个锁对象，调用lock方法和unlock方法）
* 单例模式的另一种线程安全的实现：双重校验锁DCL(double-checked locking）(JDK1.5+)

  ```java
  public class Singleton {  
      private volatile static Singleton singleton;  
      private Singleton (){}  
      public static Singleton getSingleton() {  
      if (singleton == null) {  
          synchronized (Singleton.class) {  
              if (singleton == null) {  
                  singleton = new Singleton();  
              }  
          }  
      }  
      return singleton;  
      }  
  }
  ```

#### 比较器

* 自然排序：在该类中实现java.lang.Comparable接口并重写其中方法int compareTo(Object o)
* 定制排序：单独实现java.util.Comparator接口并重写其中方法int compare(Object o1,Object o2)

#### 枚举类(JDK 1.5+)

* 用enum关键字修饰，等效于继承了java.lang.Enum类
* 类中第一行为枚举常量列表（等价于创建一系列public static final的类对象） `【枚举常量名1】(【属性成员值1】,【属性成员值2】...),...;`
* 属性成员为private final，构造器为private；属性成员应在构造器中赋值
* 类方法
  * toString()返回当前对象的枚举常量名
  * 静态的values()返回枚举类的枚举常量数组
  * 静态的valueOf(String str)返回字符串对应的枚举常量名的一个枚举类对象
* 枚举类实现接口时，可针对每个枚举常量在枚举常量列表处分别重写接口的方法

#### 注解Annotation(JDK 1.5+)

* 格式：@...
* 可修饰一切对象
* 这些标记可以在编译, 类加载, 运行时被其他工具读取并执行相应的处理
* 在开发中用于代替JavaEE旧版中所遗留的繁冗代码和XML配置等，是一种趋势
* 框架 = 注解 + 反射 + 设计模式
* 用于生成文档：@author @version @see @since @param @return @exception...
* 用于格式检查：@Override重写 @Deprecated已过时 @SuppressWarnings抑制编译器警告...
* 用于跟踪代码依赖性，实现替代配置文件功能：
* 自定义注解：`public @interface 【注解名】{...}`
* 没有成员定义的 Annotation 称为标记; 包含成员变量的 Annotation 称为元数据
* 用反射读取注解并执行信息处理流程：使用java.lang.reflect包下 AnnotatedElement 接口来读取注解
* 元注解（用于修饰注解）

  * Retention：指定注解的生命周期
  * Target：指定注解能修饰哪些对象
  * Documented：指定注解在被javadoc解析时保留下来
  * Inherited：指定注解的继承性
  * Repeatable(jdk1.8)：指定注解可重复修饰对象

#### 迭代器Iterator

定义为java.util.Iterator接口。

* 可作为一种设计模式：提供一种方法访问一个容器(container)对象中各个元素，而又不需暴露该对象的内部细节。
* 方法：forEachRemaining、hasNext、next、remove、forEach(java8)

#### foreach(JDK 1.5+)

for(【数据类型】 【迭代变量名】: 【迭代集合】) {...}

底层用迭代器实现。

#### 容器类/集合

##### Collection接口

* 之前Java 集合会丢失容器中所有对象的数据类型，把所有对象都当成 Object 类型处理；从 JDK 5.0 增加了泛型以后，Java 集合可以记住容器中对象的数据类型。
* 成员方法：增删改查、toArray()、hashcode()、iterator()、静态方法unmodifiablexxx()
* 继承了java.lang.Iterable接口，内含iterator()方法，返回迭代器

###### List子接口（有序可重复）

* 可用索引
* 常用方法：add、addAll、get、indexOf、remove、set、subList

**常用实现类：**

**Vector（基本过时）**

底层实现：数组封装。每次扩容2倍。线程安全的。初始容量为10。

新增方法：addElement、insertElementAt、setElementAt、removeElement、removeAllElements

子类：Stack

**ArrayList（最常用）**

底层实现：数组封装。每次扩容1.5倍。线程不安全的。（JDK1.7：ArrayList像饿汉式，直接创建一个初始容量为10的数组；JDK1.8：ArrayList像懒汉式，一开始创建一个长度为0的数组，当添加第一个元素时再创建一个始容量为10的数组）。

Arrays.asList()返回的是一个只读的List集合（底层是仅重写了ArrayList的get和set方法的内部类）。java8支持将该其强制转换成一个普通的ArrayList。

**LinkedList**

底层实现：双向链表

新增方法：addFirst、addLast、 getFirst、getLast、removeFirst、removeLast

###### Set子接口（无序不可重复）

没有新增方法

实现了equals()

**常用实现类：**

**HashSet（最常用）**

底层实现：hashmap（作为key存储，value指向一个同一个空object对象）

使用哈希算法存储。线程不安全的。可存空元素。

判断元素是否重复时，先调用hashCode()，再调用equals()。

用数组存储，初始长度16。jdk7饿汉式，jdk8懒汉式。

同位置多个元素以链表存储，jdk7新元素作为头节点，jdk8原元素作为头节点。

hashCode重写模板中常用31作为膨胀系数：一方面取尽量接近2的幂（左移实现）的合适大小，另一方面取素数避免冲突。

**LinkedHashSet（HashSet子类）**

在HashSet基础上为每个元素维护头尾指针，实现双向链表的效果，便于遍历。

**SortedSet子接口（实现类为TreeSet）**

保证元素排序性，新增方法：first、last、headSet、tailSet、subSet、comparator

TreeSet底层实现用红黑树存储，默认自然排序，判断重复性时仍根据比较器而非调用equals；需用定制排序时将比较器传入构造器；新增方法：higher、lower

```java
HashSet set = new HashSet();
Person p1 = new Person(1001,"AA");
Person p2 = new Person(1002,"BB");
set.add(p1);
set.add(p2);
p1.name = "CC";
set.remove(p1);
System.out.println(set);
set.add(new Person(1001,"CC"));
System.out.println(set);
set.add(new Person(1001,"AA"));
System.out.println(set);

```

##### Map接口

key和value封装成内部接口Entry存储，无序不可重复，故key和value需重写equals().

方法：put、putAll、remove、clear、get、containsKey、containsValue、keySet、entrySet、values

**实现类：**

###### Hashtable（基本过时）

线程安全的。非空值。

底层实现类似于HashMap。

子类Properties：key value都是String

###### HashMap（最常用）

线程不安全的。允许空值。默认初始数组长度DEFAULT_INITIAL_CAPACITY=16，指定数组长度初始化时会容量会扩展为2的幂，超过临界值threshold（DEFAULT_LOAD_FACTOR=0.75xCapacity且新增元素位置不为空，默认2倍扩容resize，扩容后需重新计算更新各元素位置。

底层实现：

* jdk7：饿汉式；Entry数组+链表；新元素作为链表头节点；
* jdk8：懒汉式；Node数组+链表/红黑树（当此位置上链表长度大于TREEIFY_THRESHOLD=8且数组长度大于64时转换为红黑树，当红黑树节点数小于UNTREEIFY_THRESHOLD=6时转换为链表）；原元素作为链表头节点；

插入操作若key相同，更新value。

子类LinkedHashSet在此基础上为每个元素维护头尾指针（Entry继承于Node），实现双向链表的效果，便于遍历。

###### SortedMap（实现类为TreeMap）

TreeSet底层实现用红黑树存储；默认自然排序，判断重复性时仍根据比较器而非调用equals；需用定制排序时将比较器传入构造器；

###### CurrentMap接口及其实现类ConcurrentMap（线程安全）？

##### java.util.Collections工具类

一系列操作集合静态方法：swap、reverse、shuffle、sort、max、min、frequency、copy、replaceAll、synchronizedXxx() 转换为线程同步集合

#### 泛型(jdk5+)

* 类似cpp类模板
* 不能用基本数据类型，需替换为其包装类。
* jdk8增加了类型推断。
* 定义异常类不能使用泛型。
* A继承B，泛型结构 `<A>`并不继承泛型结构 `<B>`。
* 类型通配符：?，可以看作任意类型的父类；有限制的通配符：? extends...和? super...

#### IO流

java.io

##### 文件类File

一系列常用方法

##### 流类

图？IO流体系

flush()清空缓冲区（将当前遗留在缓冲区的数据完全读写）

###### 抽象基类

InputStream（字节流）、OutputStream（字节流）、Reader（字符流）、Writer（字符流）

###### 节点流（文件流）Filexxx

###### 处理流（其余流类）

对文件流进行包装，实现特定功能

**缓冲流Bufferedxxx**

加快读写效率

**转换流**

InputStreamReader OutputStreamWriter

将字节流转换为字符流

**标准输入输出流**

java.lang.System类中

静态成员in类型为InputStream，out和err类型为PrintStream（OutputStream的子类）

静态方法setIn、setOut可重定向

**打印流**

PrintStream PrintWriter

重载了一系列print方法

**数据流**

DataInputStream DataOutputStream

针对基本数据类型和String不同数据类型重载了一系列读写方法，方便内存与数据源之间的数据读写，读写顺序需一致。

**对象流**

ObjectInputStream OjbectOutputSteam

作用于可序列化对象，实现内存与数据源之间的以对象为单位的数据读写，读写顺序需一致。

##### Serializable接口

表示可序列化：可将对象按照一定规则转换成二进制字节流

空方法的标识接口，静态成员serialVersionUID标识类的版本号，默认情况下java根据类的结构自动生成，建议显式定义

可序列化的类的对象的每个成员也必须是可序列化的，transient修饰的成员不进行序列化（数据丢失）

##### RandomAccessFile流类

直接继承于object而非上述四大流基类，实现DataInput接口和DataOutput接口

支持 “随机访问”，可指定读写模式，类似于cpp

getFilePointer()获取文件记录指针的当前位置

seek(long pos)将文件记录指针定位到 pos 位置

##### java.NIO

Java 1.4引入的一套新的IO API，是面向缓冲区的、基于通道的IO操作，更加高效，常用于网络编程。

核心组件有Channel，Buffer和Selector

java1.7扩展为NIO.2，引入Path接口替代File类、工具类Files和Paths

#### 反射

反射机制允许程序在执行期借助于Reflection API取得任何类的内部信息，并能直接操作任意对象的内部属性及方法。

动态语言：在运行时代码可以根据某些条件改变自身结构，如Object-C、C#、JavaScript、PHP、Python、Erlang。java是静态语言但可通过反射机制体现一定的动态性。

##### java.lang.Class类

描述一切类（类、接口、数组、枚举、注解、基本数据类型）的类

通过Class对象可以看到对应类的内部结构，可通过一系列getxxx方法返回该类及其父类的public结构，可通过一系列getDeclarexxx方法返回该类所有结构。

**类的调用过程：**

1. 加载：当程序使用某个类时，加载器ClassLoader将.class文件读入内存中（静态数据转换成方法区的运行时数据结构），并在堆内存中就产生了一个Class类对象作为方法区的入口引用地址
2. 链接：将类的二进制数据合并到JRE中，又包括验证、准备、解析
3. 初始化：JVM执行类构造器()方法的过程
4. 回收：类在加载之后可以缓存一段时间，可被JVM回收

**获取类的Class对象的方法：**

1. 【类名】.class静态属性
2. Object.getClass()方法
3. Class.forName(【类名】)静态方法

newInstance()方法可调用运行时类的空参构造器创建对象

##### java.lang.reflect

下属的描述类的结构的组件有Method方法类（内含invoke方法）、Field成员变量类（内含get set 方法）、Constructor构造器类

所有对象都有setAccessible(boolean)方法设置是否进行访问权限检查

##### 动态代理 （java.lang.reflect.Proxy类）

使用反射根据运行时的被代理类及其接口动态创建一个代理类实现代理，以优化静态代理中每一个代理类只能为一个接口服务的弊端。

常用结构：Proxy.newProxyInstance静态方法以及InvocationHandler接口

```java
//动态创建代理类
class ProxyFactory{
	public static getProxyInstance(Object obj){
		MyInvocationHandler myInvocationHandler = new MyInvocationHandler(obj);
		Proxy.newProxyInstance(obj.getClass().getClassLoader(),obj.getClass().getInterfaces(),myInvocationHandler);
	}
}
//实现代理类调用被代理类的同名方法（绑定）
class MyInvocationHandler implements InvocationHandler{
	private Object obj;
	public MyInvocationHandler (Object obj) {this.obj = obj;}
	@Override
	public object invoke(Object proxy,Method method,object[] args)throws Throwable{
		...//可自定义的附加操作
		return method.invoke(obj,args);
	}
}
//运行时类及其实现的接口
class 【被代理类】implements 【接口名】{
	...
	@Override
	【重载的接口方法】
	...
}
//运行线程
public class ProxyMain{
	public static void main(String[] args){
	【被代理类】【被代理类对象】=new 【被代理类】();
	Object 【代理类对象】= ProxyFactory.getProxyInstance(【被代理类对象】);
	【代理类对象】.【接口方法名】;
	}
}
```

AOP应用于动态代理中：在InvocationHandler.invoke()中既定义了动态操作，又可以自定义其他通用的附加操作。

#### 函数式接口(java8)

只包含一个抽象方法的接口

可用@FunctionalInterface 注解标识

在java.util.function包下定义了Java 8 的丰富的函数式接口，其中常用的有：`Consumer <T>{void accept(T t)}、Supplier <T>{T get()}、Function <R,T>{R apply(T t)}、Predicate <T>{boolean test(T t)}`

#### Lambda表达式(java8)

一种简化版的语法，用于创建匿名函数式接口对象。这个对象可以看作是一个可传递的匿名函数，体现了OOF面向函数编程。

`(【参数列表】)->{【重写的抽象方法体】}`

当重写的抽象方法已存在时，Lambda表达式可再简化为 `【所属类/对象】::【方法名】`，称为方法引用，其中构造器引用为 `【类名】::new`

#### Stream API (java8)

java.util.stream类及其子类如IntStream、DoubleStream...

支持指定对集合查找、过滤和映射数据等操作，且该操作是延迟执行/惰性求值的（调用终止操作时才会执行中间的连续调用的操作链），一旦执行终止操作stream对象不可再复用。

把真正的函数式编程风格引入到Java中

##### 创建stream对象的方法

1. Collection 接口中新增的默认方法：stream() 顺序流、parallelStream()并行流
2. Arrays.stream(【数组】)
3. Stream.of()
4. Stream.iterate() 和 Stream.generate() 创建无限流

##### stream对象的中间操作方法

* 筛选切片：filter(Predicate p)、distinct()、limit(long maxSize)、skip(long n)
* 映射：map(Function f)、mapToxxx()、flatMap(Function f)将流中的每个值都换成另一个流,然后把所有流连接成一个流
* 排序：sorted()

##### stream对象的终止操作方法（返回结果）

* 自定义匹配：all/any/noneMatch(Predicate p)
* 自定义迭代：forEach(Consumer c)
* 直接返回：findFirst/Any()、count()、max/min(Comparator c)
* 归约：reduce(BinaryOperator b)将流元素两两反复运算返回一个结果
* 自定义收集：collect(Collector c)，常把java.util.stream.Collectors工具类中处理流的静态方法作为传入参数

#### Optional `<T>`类(java8)

java.util.Optional是一个容器类，保存T类型值或null，旨在减少空指针异常。

创建对象：使用其静态方法of(T t)、empty()、ofNullable(T t)

其他常用方法：isPresent()、get()、orElse(...)

#### java9新特性

##### jdk目录结构的变化

##### 模块化系统Modularity(java9)

源自Jigsaw项目

引入模块module作为工程与包之间的一层结构。

默认不同模块之间不能相互访问，需要访问时需加上requires...和exports...

##### REPL工具： jShell命令

支持直接在控制台执行代码，无需创建java文件和类

##### 接口的私有方法

##### try语句中资源的自动关闭

不再需要在finall里手动关闭

java8：将资源初始化语句转移到try后的()内

java9：将需要关闭的资源传入到try后的()内

##### String底层存储结构由char[]改为byte[]

char[]存储时每个字符均用两个byte存储

byte[]增加一个flag，存储拉丁字符用一个byte，其他有需要可用2byte

##### 快速创建只读集合

List、Set、Map的静态方法of()

##### transferTo()

`【InputStream对象】.transferTo(【OutputStream对象】)`，把输入流中的所有数据直接自动地复制到输出流中

##### Stream增强

新增方法：takeWhile(Predicate)、dropWhile(Predicate)、 静态的ofNullable，重载了iterate()方法可传入终止条件

通过 Optional 的新方法 stream() 将一个 Optional 对象转换为一个(可能是空的) Stream 对象

Optional的stream()

#### java10新特性

##### 局部变量类型推断

声明并初始化变量时可用var，将根据初始化赋值语句右值自动推断类型

##### copyOf()

List / Set / Map新增的创建只读集合的静态方法（若本身即为只读的则返回本身）

#### java11新特性（LTS）

##### String新增方法

如isBlank()、.strip()、.repeat(n)、.lines().count()

常用于字符串字面量

##### HTTP Client API

java.net

将 替 代 仅 适 用 于 blocking 模式的 HttpURLConnection，并提供对WebSocket 和 HTTP/2的支持

##### ZGC

A Scalable Low-Latency Garbage Collector(Experimental)

是一个并发, 基于region, 压缩型的垃圾收集器, 旨在减少GC停顿时长。

### JVM

## 图形界面javafx

## JDBC

## java下的网络编程

## javaweb
