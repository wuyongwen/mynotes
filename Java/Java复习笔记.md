---
typora-root-url: ../../mynotes
---

[TOC]
# Java基础

## Java 的两大数据类型

1. 内置数据类型

    八种基本类型(六种数据类型，一种字符型，一种布尔型)

   byte, short, int, long, float, double, boolean, char

2. 引用数据类型

   string , 引用类型指向一个对象，指向对象的变量是引用变量。这些变量在声明时被指定为一个特定的类型，比如 Employee、Puppy 等。变量一旦声明后，类型就不能被改变了。

## 类型转换

1. 自动类型转换从低级到高级。

   整型、实型（常量）、字符型数据可以混合运算。运算中，不同类型的数据先转化为同一类型，然后进行运算。

```
低  ------------------------------------>  高

byte,short,char—> int —> long—> float —> double 
```

2. 强制类型转换

   转换的数据类型必须是兼容的。

3. 隐含强制类型转换

   整数的默认类型是int。

## 变量类型

1. 局部变量

   - 局部变量声明在方法、构造方法或者语句块中；
   - 局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；

   - 访问修饰符不能用于局部变量；

   - 局部变量只在声明它的方法、构造方法或者语句块中可见；

   - 局部变量是在栈上分配的。

   - 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。

2. 实例变量

   - 实例变量声明在一个类中，但在方法、构造方法和语句块之外；
   - 当一个对象被实例化之后，每个实例变量的值就跟着确定；
   - 实例变量在对象创建的时候创建，在对象被销毁的时候销毁；
   - 实例变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息；
   - 实例变量可以声明在使用前或者使用后；
   - 访问修饰符可以修饰实例变量；
   - 实例变量对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把实例变量设为私有。通过使用访问修饰符可以使实例变量对子类可见；
   - 实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在构造方法中指定；
   - 实例变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObejectReference.VariableName。

3. 类变量(静态变量)

   - 类变量也称为静态变量，在类中以 static 关键字声明，但必须在方法之外。

   - 无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。

   - 静态变量除了被声明为常量外很少使用。常量是指声明为public/private，final和static类型的变量。常量初始化后不可改变。

   - 静态变量储存在静态存储区。经常被声明为常量，很少单独使用static声明变量。

   - 静态变量在第一次被访问时创建，在程序结束时销毁。

   - 与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为public类型。

   - 默认值和实例变量相似。数值型变量默认值是0，布尔型默认值是false，引用类型默认值是null。变量的值可以在声明的时候指定，也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。

   - 静态变量可以通过：*ClassName.VariableName*的方式访问。

   - 类变量被声明为public static final类型时，类变量名称一般建议使用大写字母。如果静态变量不是public和final类型，其命名方式与实例变量以及局部变量的命名方式一致。

## 修饰符

### 访问控制修饰符

- **default** (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。不同包子类不可见

- **private** : 在同一类内可见。使用对象：变量、方法。并且类和接口不能声明为 **private**。 **注意：不能修饰类（外部类）**

- **public** : 对所有类可见。使用对象：类、接口、变量、方法。接口里的变量都隐式声明为 **public static final**,而接口里的方法默认情况下访问权限为 **public**。

- **protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**。非子包中只可通过继承重写方法，无法调用父类实例方法。

  |  修饰符   | 当前类 | 同一包 | 子孙类（同一包） | 子孙类（不同包） | 其他包 |
  | :-------: | :----: | :----: | :--------------: | :--------------: | :----: |
  |  public   |   Y    |   Y    |        Y         |        Y         |   Y    |
  | protected |   Y    |   Y    |        Y         |       Y/N        |   N    |
  |  default  |   Y    |   Y    |        Y         |        N         |   N    |
  |  private  |   Y    |   N    |        N         |        N         |   N    |

#### 访问控制和继承

- 父类中声明为 public 的方法在子类中也必须为 public。
- 父类中声明为 protected 的方法在子类中要么声明为 protected，要么声明为 public，不能声明为 private。
- 父类中声明为 private 的方法，不能够被继承。

### 非访问修饰符

- static 修饰符，用来修饰类方法和类变量。

- final 修饰符，用来修饰类、方法和变量，final 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。

- abstract 修饰符，用来创建抽象类和抽象方法。一个类不能同时被 abstract 和 final 修饰。

- synchronized 和 volatile 修饰符，主要用于线程的编程。synchronized 关键字声明的方法同一时间只能被一个线程访问。volatile 修饰的成员变量在每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。而且，当成员变量发生变化时，会强制线程将变化值回写到共享内存。这样在任何时刻，两个不同的线程总是看到某个成员变量的同一个值。

- transient 修饰符，序列化的对象包含被 transient 修饰的实例变量时，java 虚拟机(JVM)跳过该特定的变量。

   该修饰符包含在定义变量的语句中，用来预处理类和变量的数据类型。

## Java运算符

#### 运算符分类

- 算数运算符
- 关系运算符
- 位运算符
- 逻辑运算符
- 赋值运算符
- 条件运算符 （三元运算符）
- instanceof运算符 ( Object reference variable ) instanceof  (class/interface type)

#### 运算符优先级

Java 语言中运算符的优先级共分为 14 级，其中 1 级最高，14 级最低。在同一个表达式中运算符优先级高的先执行。表 1 列出了所有的运算符的优先级以及结合性。

| 优先级 | 运算符                                           |  结合性  |
| :----: | ------------------------------------------------ | :------: |
|   1    | ()、[]、{}                                       | 从左向右 |
|   2    | !、+、-、~、++、--                               | 从右向左 |
|   3    | *、/、%                                          | 从左向右 |
|   4    | +、-                                             | 从左向右 |
|   5    | «、»、>>>                                        | 从左向右 |
|   6    | <、<=、>、>=、instanceof                         | 从左向右 |
|   7    | ==、!=                                           | 从左向右 |
|   8    | &                                                | 从左向右 |
|   9    | ^                                                | 从左向右 |
|   10   | \|                                               | 从左向右 |
|   11   | &&                                               | 从左向右 |
|   12   | \|\|                                             | 从左向右 |
|   13   | ?:                                               | 从右向左 |
|   14   | =、+=、-=、*=、/=、&=、\|=、^=、~=、«=、»=、>>>= | 从右向左 |

## Java switch case 语句

1. switch case 执行时，一定会先进行匹配，匹配成功返回当前 case 的值，再根据是否有 break，判断是否继续输出，或是跳出判断。

2. 如果 case 语句块中没有 break 语句时，JVM 并不会顺序输出每一个 case 对应的返回值，而是继续匹配，匹配不成功则返回默认 case。

3. 如果 case 语句块中没有 break 语句时，匹配成功后，从当前 case 开始，后续所有 case 的值都会输出。

4. 如果当前匹配成功的 case 语句块没有 break 语句，则从当前 case 开始，后续所有 case 的值都会输出，如果后续的 case 语句块有 break 语句则会跳出判断。

   ```java
   public class Test {
      public static void main(String args[]){
         int i = 1;
         switch(i){
            case 0:
               System.out.println("0");
            case 1:
               System.out.println("1");
            case 2:
               System.out.println("2");
            case 3:
               System.out.println("3"); break;
            default:
               System.out.println("default");
         }
      }
   }
   ```

   ```java
   1
   2
   3
   ```

## 数组

* 数组的定义

  Java 中定义数组的语法有两种：
    type arrayName[];
    type[] arrayName;

* 数组的初始化

  声明数组的同时进行初始化（静态初始化），也可以在声明以后进行初始化（动态初始化）

  ```java
  public class Test {
      public static void main(String[] args) {
          int score[] = null; // 【1】声明数组，但未开辟堆内存
          score = new int[3]; // 【2】为数组开辟堆内存空间，大小为3
          for (int x = 0; x < score.length; x++) { // 数组的长度可以用“数组名.length”
              score[x] = x * 2 + 1 ; // 为每一个元素赋值
          } // 【3】开辟堆内存空间结束
          for (int x = 0; x < 3; x++) { // 使用循环依次输出数组中的全部内容
              System.out.println("score[" + x + "] = " + score[x]);
          }
      }
  }
  ```
【1】【2】【3】处分别对应下面这三张图：

  ![img](/img/70.png)![img](/img/71.png)![img](/img/72.png)

  

## Java 方法

### 方法的定义

- **修饰符：**修饰符，这是可选的，告诉编译器如何调用该方法。定义了该方法的访问类型。

- **返回值类型 ：**方法可能会返回值。returnValueType 是方法返回值的数据类型。有些方法执行所需的操作，但没有返回值。在这种情况下，returnValueType 是关键字**void**。

- **方法名：**是方法的实际名称。方法名和参数表共同构成方法签名。
- **参数类型：**参数像是一个占位符。当方法被调用时，传递值给参数。这个值被称为实参或变量。参数列表是指方法的参数类型、顺序和参数的个数。参数是可选的，方法可以不包含任何参数。
- **方法体：**方法体包含具体的语句，定义该方法的功能。

![img](/img/12-130Q1220955916.jpg)

### 方法的值传递

在Java中所有的参数传递，不管基本类型还是引用类型，都是值传递，或者说是副本传递。

**如果是对基本数据类型的数据进行操作，由于原始内容和副本都是存储实际值，并且是在不同的栈区，因此形参的操作，不影响原始内容。**

**如果是对引用类型的数据进行操作，分两种情况，一种是形参和实参保持指向同一个对象地址，则形参的操作，会影响实参指向的对象的内容。一种是形参被改动指向新的对象地址（如重新赋值引用），则形参的操作，不会影响实参指向的对象的内容。** 

> [Java的值传递]: https://zhuanlan.zhihu.com/p/55548266



### finalize() 方法

Java 允许定义这样的方法，它在对象被垃圾收集器析构(回收)之前调用，这个方法叫做 finalize( )，它用来清除回收对象。

例如，你可以使用 finalize() 来确保一个对象打开的文件被关闭了。

在 finalize() 方法里，你必须指定在对象销毁时候要执行的操作。

### 可变参数

JDK 1.5 开始，Java支持传递同类型的可变参数给一个方法。

方法的可变参数的声明如下所示：

typeName... parameterName

在方法声明中，在指定参数类型后加一个省略号(...) 。

一个方法中只能指定一个可变参数，它必须是方法的最后一个参数。任何普通的参数必须在它之前声明。



## Java IO操作

### IO相关类

![img](/img/iostream2xx.png)

1. 文件流：FileInputStream/FileOutputStream， FileReader/FileWriter

   这四个类是专门操作文件流的，用法高度相似，区别在于前面两个是操作字节流，后面两个是操作字符流。它们都会直接操作文件流，直接与OS底层交互。因此他们也被称为**节点流**。

   注意使用这几个流的对象之后，需要关闭流对象，因为java垃圾回收器不会主动回收。不过在Java7之后，可以在 try() 括号中打开流，最后程序会自动关闭流对象，不再需要显示地close。

2. 包装流：PrintStream/PrintWriter/Scanner

   PrintStream可以封装（包装）直接与文件交互的节点流对象OutputStream, 使得编程人员可以忽略设备底层的差异，进行一致的IO操作。因此这种流也称为处理流或者包装流。

   PrintWriter除了可以包装字节流OutputStream之外，还能包装字符流Writer

   Scanner可以包装键盘输入，方便地将键盘输入的内容转换成我们想要的数据类型。

3. 字符串流：StringReader/StringWriter

   这两个操作的是专门操作String字符串的流，其中StringReader能从String中方便地读取数据并保存到char数组，而StringWriter则将字符串类型的数据写入到StringBuffer中（因为String不可写）。

4. 转换流：InputStreamReader/OutputStreamReader

   这两个类可以将字节流转换成字符流，被称为字节流与字符流之间的桥梁。我们经常在读取键盘输入(System.in)或网络通信的时候，需要使用这两个类

5. 缓冲流：BufferedReader/BufferedWriter ， BufferedInputStream/BufferedOutputStream

   没有经过Buffered处理的IO， 意味着每一次读和写的请求都会由OS底层直接处理，这会导致非常低效的问题。

   经过Buffered处理过的输入流将会从一个buffer内存区域读取数据，本地API只会在buffer空了之后才会被调用（可能一次调用会填充很多数据进buffer）。

   经过Buffered处理过的输出流将会把数据写入到buffer中，本地API只会在buffer满了之后才会被调用。

   BufferedReader/BufferedWriter可以将字符流(Reader)包装成缓冲流，这是最常见用的做法。

   另外，**BufferedReader提供一个readLine()可以方便地读取一行**，而FileInputStream和FileReader只能读取一个字节或者一个字符，因此BufferedReader也被称为行读取器。



## Java 异常处理

### 简介

- Java异常是Java提供的一种识别及响应错误的一致性机制。
- Java异常机制可以使程序中异常处理代码和正常业务代码分离，保证程序代码更加优雅，并提高程序健壮性。在有效使用异常的情况下，异常能清晰的回答what, where, why这3个问题：异常类型回答了“什么”被抛出，异常堆栈跟踪回答了“在哪“抛出，异常信息回答了“为什么“会抛出。

- Java异常机制用到的几个关键字：**try、catch、finally、throw、throws。**
  1. **try**     -- 用于监听。将要被监听的代码(可能抛出异常的代码)放在try语句块之内，当try语句块内发生异常时，异常就被抛出。
  2.  **catch**  -- 用于捕获异常。catch用来捕获try语句块中发生的异常。
  3.  **finally** -- finally语句块总是会被执行。它主要用于回收在try块里打开的物力资源(如数据库连接、网络连接和磁盘文件)。只有finally块，执行完成之后，才会回来执行try或者catch块中的return或者throw语句，如果finally中使用了return或者throw等终止方法的语句，则就不会跳回执行，直接停止。
  4.  **throw**  -- 用于抛出异常。
  5.  **throws** -- 用在方法签名中，用于声明该方法可能抛出的异常。

### Java异常框架

Java异常架构图

![img](/img/111228085926220.jpg)



1. **Throwable ** 

   Throwable是 Java 语言中所有错误或异常的超类。
   Throwable包含两个子类: **Error** 和 **Exception**。它们通常用于指示发生了异常情况。
   Throwable包含了其线程创建时线程执行堆栈的快照，它提供了printStackTrace()等接口用于获取堆栈跟踪数据等信息。

2. **Exception**
   Exception及其子类是 Throwable 的一种形式，它指出了合理的应用程序想要捕获的条件。

3. **RuntimeException**
   RuntimeException是那些可能在 Java 虚拟机正常运行期间抛出的异常的超类。
   编译器不会检查RuntimeException异常。例如，除数为零时，抛出ArithmeticException异常。RuntimeException是ArithmeticException的超类。当代码发生除数为零的情况时，倘若既"没有通过throws声明抛出ArithmeticException异常"，也"没有通过try...catch...处理该异常"，也能通过编译。这就是我们所说的"编译器不会检查RuntimeException异常"！
   如果代码会产生RuntimeException异常，则需要通过修改代码进行避免。例如，若会发生除数为零的情况，则需要通过代码避免该情况的发生！

4. **Error**和Exception一样，Error也是Throwable的子类。它用于指示合理的应用程序不应该试图捕获的严重问题，大多数这样的错误都是异常条件。
   和RuntimeException一样，编译器也不会检查Error。

![image-20200322161214495](/img/image-20200322161214495.png)

Java将可抛出(Throwable)的结构分为三种类型：**被检查的异常(Checked Exception)，运行时异常(RuntimeException)和错误(Error)。**

1. **运行时异常**
   **定义**: RuntimeException及其子类都被称为运行时异常。
   **特点**: Java编译器不会检查它。也就是说，当程序中可能出现这类异常时，倘若既"没有通过throws声明抛出它"，也"没有用try-catch语句捕获它"，还是会编译通过。例如，除数为零时产生的ArithmeticException异常，数组越界时产生的IndexOutOfBoundsException异常，fail-fail机制产生的ConcurrentModificationException异常等，都属于运行时异常。
   　　虽然Java编译器不会检查运行时异常，但是我们也可以通过throws进行声明抛出，也可以通过try-catch对它进行捕获处理。
   　　如果产生运行时异常，则需要通过修改代码来进行避免。例如，若会发生除数为零的情况，则需要通过代码避免该情况的发生！

   ClassCastException ，ArrayIndexOutOfBoundsException，NullPointerException，BufferOverflowException， IllegalArgumentException

2. **被检查的异常**
   **定义**: Exception类本身，以及Exception的子类中除了"运行时异常"之外的其它子类都属于被检查异常。
   **特点**: Java编译器会检查它。此类异常，要么通过throws进行声明抛出，要么通过try-catch进行捕获处理，否则不能通过编译。例如，CloneNotSupportedException就属于被检查异常。当通过clone()接口去克隆一个对象，而该对象对应的类没有实现Cloneable接口，就会抛出CloneNotSupportedException异常。

   这样的异常一般是由程序的运行环境导致的。因为程序可能被运行在各种未知的环境下，而程序员无法干预用户如何使用他编写的程序，于是程序员就应该为这样的异常时刻准备着。如SQLException , IOException,ClassNotFoundException 等。

   被检查异常通常都是可以恢复的。

3. **错误**
   **定义**: Error类及其子类。
   **特点**: 和运行时异常一样，编译器也不会对错误进行检查。
   　　当资源不足、约束失败、或是其它程序无法继续运行的条件发生时，就产生错误。程序本身无法修复这些错误的。例如，VirtualMachineError就属于错误。
   　　按照Java惯例，我们是不应该是实现任何新的Error子类的！

对于上面的3种结构，我们在抛出异常或错误时，到底该哪一种？《Effective Java》中给出的建议是：对于可以恢复的条件使用被检查异常，对于程序错误使用运行时异常。



## Java 面向对象

### 继承

- 子类拥有父类非 private 的属性、方法。
- 子类可以拥有自己的属性和方法，即子类可以对父类进行扩展。

- 子类可以用自己的方式实现父类的方法。

- Java 的继承是单继承，但是可以多重继承，单继承就是一个子类只能继承一个父类，多重继承就是，例如 A 类继承 B 类，B 类继承 C 类，所以按照关系就是 C 类是 B 类的父类，B 类是 A 类的父类，这是 Java 继承区别于 C++ 继承的一个特性。

- 提高了类之间的耦合性（继承的缺点，耦合度高就会造成代码之间的联系越紧密，代码独立性越差）。

### 方法的重载 重写

#### 重载（Overload）

-  方法重载是让类以统一的方式处理不同类型数据的一种手段。多个同名函数同时存在，具有不同的参数个数/类型。重载Overloading是一个类中多态性的一种表现。
- Java的方法重载，就是在类中可以创建多个方法，它们具有相同的名字，但具有不同的参数和不同的定义。调用方法时通过传递给它们的不同参数个数和参数类型来决定具体使用哪个方法, 这就是多态性。  
- 重载的时候，方法名要一样，但是参数类型和个数不一样，返回值类型可以相同也可以不相同。无法以返回型别作为重载函数的区分标准。

#### 重写（Override）

-  父类与子类之间的多态性，对父类的函数进行重新定义。如果在子类中定义某方法与其父类有相同的名称和参数，我们说该方法被重写 (Overriding)。在Java中，子类可继承父类中的方法，而不需要重新编写相同的方法。但有时子类并不想原封不动地继承父类的方法，而是想作一定的修改，这就需要采用方法的重写。方法重写又称方法覆盖。
- 若子类中的方法与父类中的某一方法具有相同的方法名、返回类型和参数表，则新方法将覆盖原有的方法。如需父类中原有的方法，可使用super关键字，该关键字引用了当前类的父类。

- 子类函数的访问修饰权限不能少于父类的；

### 动态绑定与静态绑定

#### 静态绑定

- 静态绑定（前期绑定）是指：在程序运行前就已经知道方法是属于那个类的，在编译的时候就可以连接到类的中，定位到这个方法。
- 在Java中，final、private、static修饰的方法以及构造函数都是静态绑定的，不需程序运行，不需具体的实例对象就可以知道这个方法的具体内容。

#### 动态绑定

调用的方法依赖于隐式参数的实际类型，并且在运行时实现动态绑定。动态绑定的过程分为以下几个环节：

　　（1）编译器查看对象的声明类型和方法名；

　　（2）编译器查看调用方法时提供的参数类型。例如x.f("hello")，编译器将会挑选f(String)，而不是f(int)，由于存在类型转换（int转换为double），所以可能会更复杂。如果编译器没找到参数类型匹配的方法，或者发现有多个方法与之匹配，就会报告一个错误。

　　至此，编译器获得了需要调用的方法名字和参数类型。

　　（3）采用动态绑定调用方法的时候，一定调用与所引用对象的实际类型最合适的类的方法。如果x的实际类型是D，它是C类的子类，如果D定义了一个方法f(String)，就直接调用它，否则将在D类的超类中寻找f(String)，以此类推。

​		每次调用方法都要进行搜索，时间开销太大，所以虚拟机预先为每个类创建一个方法表（method table），其中列出了所有方法的签名和实际调用的方法。这样在调用方法的时候，只需要查找这个表即可。

**与方法不同，在处理Java类中的成员变量（实例变量和类变量）时，并不是采用运行时绑定，而是一般意义上的静态绑定。所以在向上转型的情况下，对象的方法可以找到子类，而对象的属性（成员变量）还是父类的属性（子类对父类成员变量的隐藏）。**

```java
public class Father {
    protected String name = "父亲属性";
}
　　
public class Son extends Father {
    protected String name = "儿子属性";
 
    public static void main(String[] args) {
        Father sample = new Son();
        System.out.println("调用的属性：" + sample.name);
    }
}

// out:
// 父亲属性
```

### 多态

多态是同一个行为具有多个不同表现形式或形态的能力。

多态就是同一个接口，使用不同的实例而执行不同操作。

#### 多态的优点

1. 消除类型之间的耦合关系
2. 可替换性
3. 可扩充性
4. 接口性
5. 灵活性
6. 简化性

#### 多态存在的三个必要条件

1. 继承
2. 重写
3. 父类引用指向子类对象

#### 多态的实现方式

1. 重写
2. 接口

- 生活中的接口最具代表性的就是插座，例如一个三接头的插头都能接在三孔插座中，因为这个是每个国家都有各自规定的接口规则，有可能到国外就不行，那是因为国外自己定义的接口类型。
- Java中的接口类似于生活中的接口，就是一些方法特征的集合，但没有方法的实现。

3. 抽象类和抽象方法

### 抽象类

#### 抽象类总结

- 抽象类不能被实例化，但是抽象类依然有构造方法，如果被实例化，就会报错，编译无法通过。只有抽象类的非抽象子类可以创建对象。
- 抽象类中不一定包含抽象方法，但是有抽象方法的类必定是抽象类。
- 抽象类中的抽象方法只是声明，不包含方法体，就是不给出方法的具体实现也就是方法的具体功能。
- 构造方法，类方法（用 static 修饰的方法）不能声明为抽象方法。
- 抽象类的子类必须给出抽象类中的抽象方法的具体实现，除非该子类也是抽象类。
- 抽象类可以通过子类创建上转型对象。

#### 抽象类成员的特点

- 成员变量：可以为常量（例如final修饰的常量），也可以为变量；
- 静态成员变量：可以有，可以被继承，但是不会被重写
- 构造方法：上面提到过，可以有，用于子类访问父类时数据初始化；
- 成员方法：可以是抽象的成员方法（子类必须要实现重写的），也可以是非抽象的成员方法
- 静态成员方法：抽象类中可以有静态成员方法，可以被继承但不能被子类重写

#### 抽象方法概念：

用关键字 abstract 修饰的方法就是抽象方法（abstract 方法）;

如： abstract void method();

1. 抽象方法没有方法体{}；
2. 抽象方法不能和 static 关键字一起使用；如：abstract static void method();  //是错误的
3. 抽象方法不能和 final 关键字一起使用；如：abstract final void method();  //是错误的

### Java 接口

接口是抽象方法和常量值的定义的集合。接口是一种特殊的抽象类，这种抽象类里面只包含常量和方法的定义，而没有变量和方法的实现。

#### 接口总结

- 接口中的变量默认是public static final，也只能是这种，变量前的修饰符可以写也可以不写，不影响这种特性。接口无法定义实例变量。

- 接口不能实例化，但能够定义接口类型引用，并且引用多个实现该接口类型的类实例。

- Java中类仅支持单继承，不过接口支持多继承，即一个接口可以继承多个接口。接口的实现类要实现接口中所有该实现的方法。

- 接口声明的时候，如果加上关键字public，那么接口可以被任一个类进行调用，如果没有public则为友好型接口，只能被同一个包内的类进行调用。

- Java8：（1）接口可以有默认方法用default关键字修饰。（2）接口可以有静态方法（具体的方法）用static修饰方法

  java9:  接口中可以有私有方法（用private修饰）

#### 接口与抽象类

- 抽象类可以提供成员方法的实现细节，而接口中只能存在public abstract 方法；
- 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是public static final类型的；
- 接口中不能含有静态代码块以及静态方法，而抽象类可以有静态代码块和静态方法；1.8 已经改变。
- 一个类只能继承一个抽象类，而一个类却可以实现多个接口。
- 接口是一种行为的约束，描述一种能力，是对行为的抽象。抽象类描述的事物的关系，是一种耦合，是对类的抽象。

### 内部类

#### 成员内部类

```java
class Circle {
    double radius = 0;
    public Circle(double radius) {
        this.radius = radius;
    }
    class Draw {     //内部类
        public void drawSahpe() {
            System.out.println("drawshape");
        }
    }
}
```

- 成员内部类可以无条件访问外部类的所有成员属性和成员方法（包括private成员和静态成员）。

- 当成员内部类拥有和外部类同名的成员变量或者方法时，会发生隐藏现象，即默认情况下访问的是成员内部类的成员。如果要访问外部类的同名成员，需要以下面的形式进行访问：

  ```java
  外部类.this.成员变量
  外部类.this.成员方法
  ```

- 在外部类中如果要访问成员内部类的成员，必须先创建一个成员内部类的对象，再通过指向这个对象的引用来访问：

  ```java
  //第一种方式：
  Outter outter = new Outter();
  Outter.Inner inner = outter.new Inner();  //必须通过Outter对象来创建
           
  //第二种方式：
  Outter.Inner inner1 = outter.getInnerInstance(); // out 提供方法返回内部类实例
  ```

- 内部类可以拥有private访问权限、protected访问权限、public访问权限及包访问权限。

  如果成员内部类Inner用private修饰，则只能在外部类的内部访问，如果用public修饰，则任何地方都能访问；如果用protected修饰，则只能在同一个包下或者继承外部类的情况下访问；如果是默认访问权限，则只能在同一个包下访问。

- 成员内部类中不能存在任何static的变量和方法

#### 局部内部类(方法内部类)

局部内部类是定义在一个方法或者一个作用域里面的类，它和成员内部类的区别在于局部内部类的访问仅限于方法内或者该作用域内。

```java
class People{
    public People() {   
    }
}
 
class Man{
    public Man(){     
    }
    public People getWoman(){
        class Woman extends People{   //局部内部类
            int age =0;
        }
        return new Woman();
    }
}
```

* 局部内部类就像是方法里面的一个局部变量一样，是不能有public、protected、private以及static修饰符的。

* 局部内部类，如果希望访问所在方法的变量局部，那么这个局部变量必须是final的

  > 为什么用final修饰？
  >
  > 1. new来出的对象在堆内存中。
  >
  > 2. 局部变量跟着方法，在栈中。
  >
  > 3. 方法运行结束后，立即出栈，局部变量就会消失。
  >
  > 4. 但是new出来的对象还在堆中，直到垃圾回收，如果上述过程执行完毕，对象还想调用局部变量的值，无法调用。所以使用final关键字来修饰。

#### 静态内部类

静态内部类也是定义在另一个类里面的类，只不过在类的前面多了一个关键字static。

```java
class Outter {
    public Outter() {
         
    }
     
    static class Inner {
        public Inner() {
             
        }
    }
}

Outter.Inner inner = new Outter.Inner();
```

* 实例化静态内部类：B是A的静态内部类，A.B b = new A.B()。
* 静态内部类属性和方法可以声明为静态的或者非静态的。
* 静态内部类只能引用外部类的静态的属性及方法。

#### 匿名内部类

匿名内部类不能有访问修饰符和static修饰符的。

```java
scan_bt.setOnClickListener(new OnClickListener() {
             
            @Override
            public void onClick(View v) {
                // TODO Auto-generated method stub
                 
            }
        });
```

- 匿名内部类是没有访问修饰符的。
- 匿名内部类必须继承一个抽象类或者实现一个接口
- 匿名内部类中不能存在任何静态成员或方法
- 匿名内部类是没有构造方法的，因为它没有类名
- 匿名内部类只能访问局部final变量

#### 内部类的使用场景和好处

- 每个内部类都能独立的继承一个接口的实现，所以无论外部类是否已经继承了某个(接口的)实现，对于内部类都没有影响。内部类使得多继承的解决方案变得完整.
- 方便将存在一定逻辑关系的类组织在一起，又可以对外界隐藏。
- 方便编写事件驱动程序
- 方便编写线程代码

**在非静态内部类访问外部类私有成员 / 外部类访问内部类私有成员 的时候，对应的外部类 / 外部类会生成一个静态方法，用来返回对应私有成员的值，而对应外部类对象 / 内部类对象通过调用其内部类 / 外部类提供的静态方法来获取对应的私有成员的值。**

##### 避免内存泄漏

1、能用静态内部类就尽量使用静态内部类，静态内部类的对象创建不依赖外部类对象，即静态内部对象不会持有外部类对象的引用，自然不会因为静态内部类对象而导致内存泄露，所以如果你的内部类中不需要访问外部类中的一些非 static 成员，那么请把这个内部类改造成静态内部类；

2、对于一些自定义类的对象，慎用 static 关键字修饰（除非这个类的对象的声明周期确实应该很长），我们已经知道，JVM 在进行垃圾回收时会将 static 关键字修饰的一些静态字段作为 “root” 来进行存活对象的查找，所以程序中 static 修饰的对象越多，对应的 “root” 也就越多，每一次 JVM 能回收的对象就越少。

## Java 泛型

**泛型，即“参数化类型”，所操作的数据类型被指定为一个参数。**

泛型是一种编译时类型确认机制。它提供了编译期的**类型安全**，确保在泛型类型（通常为泛型集合）上只能使用正确类型的对象，避免了在运行时出现ClassCastException。

泛型的正常工作是依赖Java编译器在编译源码的时候，先进行类型检查，然后进行类型擦除并且在类型参数出现的地方插入强制转换的相关指令实现的。为什么要进行擦除呢？这是为了避免**类型膨胀**。

### 特性

* 泛型只在编译阶段有效。

```java
List<String> stringArrayList = new ArrayList<String>();
List<Integer> integerArrayList = new ArrayList<Integer>();

Class classStringArrayList = stringArrayList.getClass();
Class classIntegerArrayList = integerArrayList.getClass();

if(classStringArrayList.equals(classIntegerArrayList)){
    Log.d("泛型测试","类型相同");
}

输出结果：泛型测试: 类型相同。
```

在编译之后程序会采取去泛型化的措施。也就是说Java中的泛型，只在编译阶段有效。在编译过程中，正确检		验泛型结果后，会将泛型的相关信息擦出，并且在对象进入和离开方法的边界处添加类型检查和类型转换的		方法。也就是说，泛型信息不会进入到运行时阶段。

* 泛型没有多态

  List<?> 是一个未知类型的List，而List<Object>其实是任意类型的List。你可以把List<String>, List<Integer>赋值给List<?>，却不能把List<String>赋值给List<Object>。

### 泛型的使用

泛型有三种使用方式，分别为：泛型类、泛型接口、泛型方法

#### 泛型类

泛型类型用于类的定义中，被称为泛型类。通过泛型可以完成对一组类的操作对外开放相同的接口。最典型的就是各种容器类，如：List、Set、Map。

```java
//此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型
//在实例化泛型类时，必须指定T的具体类型
public class Generic<T>{ 
    //key这个成员变量的类型为T,T的类型由外部指定  
    private T key;

    public Generic(T key) { //泛型构造方法形参key的类型也为T，T的类型由外部指定
        this.key = key;
    }

    public T getKey(){ //泛型方法getKey的返回值类型为T，T的类型由外部指定
        return key;
    }
}
```

> * 定义的泛型类，就一定要传入泛型类型实参么？并不是这样，在使用泛型的时候如果传入泛型实参，则会根据传入的泛型实参做相应的限制，此时泛型才会起到本应起到的限制作用。如果不传入泛型类型实参的话，在泛型类中使用泛型的方法或成员变量定义的类型可以为任何的类型。
>
> - 泛型的类型参数只能是类类型，不能是简单类型。
>
> - 不能对确切的泛型类型使用instanceof操作。如下面的操作是非法的，编译时会出错。
>
>   ```java
>   if(ex_num instanceof Generic<Number>){   
>   } 
>   ```

#### 泛型接口

```java
//定义一个泛型接口
public interface Generator<T> {
    public T next();
}
```

当实现泛型接口的类，未传入泛型实参时，与泛型类的定义相同，在声明类的时候，需将泛型的声明也一起加到类中。

在实现类实现泛型接口时，如已将泛型类型传入实参类型，则所有使用泛型的地方都要替换成传入的实参类型。

#### 泛型方法

**泛型类，是在实例化类的时候指明泛型的具体类型；泛型方法，是在调用方法的时候指明泛型的具体类型** 。

泛型方法的定义和普通方法定义不同的地方在于需要在修饰符和返回类型之间加一个泛型类型参数的声明，表明在这个方法作用域中谁才是泛型类型参数；泛型方法能使方法独立于类而产生变化。

```java
/**
 * 泛型方法的基本介绍
 * @param tClass 传入的泛型实参
 * @return T 返回值为T类型
 */
public <T> T genericMethod(Class<T> tClass)throws InstantiationException ,
  IllegalAccessException{
        T instance = tClass.newInstance();
        return instance;
}
```

>  1. public 与 返回值中间<T>非常重要，可以理解为声明此方法为泛型方法。
>  2. 只有声明了<T>的方法才是泛型方法，泛型类中的使用了泛型的成员方法并不是泛型方法。
>  3. <T>表明该方法将使用泛型类型T，此时才可以在方法中使用泛型类型T。
>  4. 与泛型类的定义一样，此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型。

#####  静态方法与泛型

静态方法有一种情况需要注意一下，那就是在类中的静态方法使用泛型：**静态方法无法访问类上定义的泛型；如果静态方法操作的引用数据类型不确定的时候，必须要将泛型定义在方法上。**

即：**如果静态方法要使用泛型的话，必须将静态方法也定义成泛型方法** 。

### 泛型上下边界

在使用泛型的时候，我们还可以为传入的泛型类型实参进行上下边界的限制.

**泛型的上下边界添加，必须与泛型的声明在一起** 。

```java
<T> void func(List<? extends T> list, T t);
```

- #### 上限（extends）

  指定的类必须是继承某个类，或者实现了某个接口（不是implements），即<=

   <?  extends List>

  对象中取出值是安全的，但是往对象中设置值是不安全的。

- #### 下限（super）

  即父类或自身。>=, 一般用于下限操作

  <？ super List>

  往对象中设置值总是安全的，取出值总是不安全的。

* 无边界通配符：**？**

  使用无边界通配符可以让泛型接收任意类型的数据

> 如果一个方法的返回值、某些参数的类型依赖另一个参数的类型就应该使用泛型方法，因为被依赖的类型如果是不确定的"?"，那么其他元素就无法依赖它。
>
> 通配符 “?” 只能用在声明类型、方法参数上，不能用在定义泛型类上。

## Java 枚举

枚举是一个被命名的整型常数的集合，用于声明一组带标识符的常数。

这个枚举实际上是由**java.lang.Enum**这个类实现的，在程序中定义的枚举类型，都会隐式继承此类。并且由于java中的继承是单继承，所以我们定义的枚举就无法在继承其他类了。

枚举的修饰符主要包括 public、private 和 internal；

枚举的构造方法默认为private

枚举的常用方法

| 方法名称    | 描述                             |
| ----------- | -------------------------------- |
| values()    | 以数组形式返回枚举类型的所有成员 |
| valueOf()   | 将普通字符串转换为枚举实例       |
| compareTo() | 比较两个枚举成员在定义时的顺序   |
| ordinal()   | 获取枚举成员的索引位置           |

#### EnumMap 类

EnumMap 是专门为枚举类型量身定做的 Map 实现。虽然使用其他的 Map（如 HashMap）实现也能完成枚举类型实例到值的映射，但是使用 EnumMap 会更加高效。

HashMap 只能接收同一枚举类型的实例作为键值，并且由于枚举类型实例的数量相对固定并且有限，所以 EnumMap 使用数组来存放与枚举类型对应的值，使得 EnumMap 的效率非常高。内部使用数组实现。

## Java 集合

### 集合图

<img src="/img/875181-20160921100733106-1187286566.png" alt="img" style="zoom:120%;" />

Collection接口是集合类的根接口，Java中没有提供这个接口的直接的实现类。但是却让其被继承产生了两个接口，就是Set和List。Set中不能包含重复的元素。List是一个有序的集合，可以包含重复的元素，提供了按索引访问的方式。

Map是Java.util包中的另一个接口，它和Collection接口没有关系，是相互独立的，但是都属于集合类的一部分。Map包含了key-value对。Map不能包含重复的key，但是可以包含相同的value。

Iterator，所有的集合类，都实现了Iterator接口，这是一个用于遍历集合中元素的接口，主要包含以下三种方法：

1. hasNext()是否还有下一个元素。
2. next()返回下一个元素。
3. remove()删除当前元素。

### Collection

#### List

##### ArrayList

```java
public class ArrayList<E> extends AbstractList<E>
     implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```

List接口扩展自Collection，它可以定义一个允许重复的有序集合，从List接口中的方法来看，List接口主要是增加了面向位置的操作，允许在指定位置上操作元素，同时增加了一个能够双向遍历线性表的新列表迭代器ListIterator。AbstractList类提供了List接口的部分实现，AbstractSequentialList扩展自AbstractList，主要是提供对链表的支持。

底层使用**数组**存储元素，这个数组可以动态创建，如果元素个数超过了数组的容量，那么就创建一个更大的新数组，并将当前数组中的所有元素都复制到新数组中。

第一次没有指定大小的话，默认生成长度为0的数组，添加元素时初始化为长度为10的数组。数组增长新长度是旧长度加上旧长度的0.5，所以**ArrayList底层数组每次扩容的大小都是1.5倍**。

删除元素时没有数组没有缩减。设定为null，等待GC回收。

##### Verctor

```java
public class Vector<E> extends AbstractList<E>
    implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```

Verctor底层使用**数组**存储元素，初始化参数可以指定默认大小和自增大小。没有指定的话默认初始化大小为 10，自增大小为0。**扩容时如果自增大小为0就扩容原数组的2倍**，否则扩容为原长度+自增大小。 

##### LinkedList

```java
public class LinkedList<E> extends AbstractSequentialList<E>
		implements List<E>, Deque<E>, Cloneable, java.io.Serializable
```

底层使用**双向链表**存储元素

```java
//存储的元素个数
transient int size = 0;
//头节点
transient Node<E> first;
//尾节点
transient Node<E> last;
```

##### **Stack 类**

　　Stack继承自Vector，实现一个后进先出的堆栈。Stack提供5个额外的方法使得Vector得以被当作堆栈使用。基本的push和pop 方法，还有peek方法得到栈顶的元素，empty方法测试堆栈是否为空，search方法检测一个元素在堆栈中的位置。Stack刚创建后是空栈。

**push**方法没有**synchronized**关键字装饰。pop，peek，search是线程安全的。

> 经常添加删除元素应该使用LinkedList, 如果在末尾添加或删除元素List效率高。查找元素List效率高与LinkedList。
>
>  vector及子类stack 是线程同步的，所以它也是线程安全的，而arraylist 是线程异步的，是不安全的。如果不考虑到线程的安全因素，一般用 arraylist效率比较高。

#### set接口

Set是一种不包含重复的元素的Collection，即任意的两个元素e1和e2都有e1.equals(e2)=false，Set最多有一个null元素。

##### HaseSet

```java
public class HashSet<E>
    extends AbstractSet<E>
    implements Set<E>, Cloneable, java.io.Serializable{
  	private transient HashMap<E,Object> map;

    // Dummy value to associate with an Object in the backing Map
    private static final Object PRESENT = new Object();
}
```

底层使用**HashMap**结构存储数据。K为放入的值，value为object() 对象。

提供 add(E e), remove(Object o),clear(), contains(Object o) , size() ,iterator() 等方法。

##### LinkedHashSet链式散列集

```java
public class LinkedHashSet<E>
    extends HashSet<E>
    implements Set<E>, Cloneable, java.io.Serializable
```

继承**HashSet**， 构造方法初始化一个**LinkedHashMap**对象，支持对规则集内的元素排序。

LinkedHashSet并没有实现SortedSet接口，它的有序性主要依赖于LinkedHashMap的有序性，所以它的有序性是指按照插入顺序保证的有序性；

LinkedHashSet在迭代访问Set中的全部元素时，性能比HashSet好，但是插入时性能稍微逊色于HashSet。Set的很多操作都是依赖Map来实现的。

##### TreeSet

```java
public class TreeSet<E> extends AbstractSet<E>
    implements NavigableSet<E>, Cloneable, java.io.Serializable
```

继承**AbstractSet**，实现了**SortedSet**接口。内部维护着一个**TreeMap**对象。TreeSet支持两种排序方式，自然排序 和定制排序，其中自然排序为默认的排序方式。向TreeSet中加入的应该是同一个类的对象。

自然排序

自然排序使用要排序元素的CompareTo（Object obj）方法来比较元素之间大小关系，然后将元素按照升序排列。

定制排序

自然排序是根据集合元素的大小，以升序排列，如果要定制排序，应该使用Comparator接口，实现 int compare(T o1,T o2)方法

#### Queue

队列是一种先进先出的数据结构，元素在队列末尾添加，在队列头部删除。Queue接口扩展自Collection，并提供插入、提取、检验等操作。

接口**Deque**，是一个扩展自Queue的双端队列，它支持在两端插入和删除元素，因为**LinkedList**类实现了Deque接口，所以通常我们可以使用LinkedList来创建一个队列。

**PriorityQueue**类实现了一个优先队列，使用**数组通过二叉小顶堆**实现，优先队列中元素被赋予优先级。PriorityQueue 队列的头指排序规则最小元素。线程不安全的队列。PriorityQueue存储的元素要求必须是可比较的对象， 如果不是就必须明确指定比较器。

> 二叉小顶堆满足以下公式
>
> ```
> leftNo = parentNo*2+1
> rightNo = parentNo*2+2
> parentNo = (nodeNo-1)/2
> ```
>
> 大顶堆：每个结点的值都大于或等于其左右孩子结点的值
> 小顶堆：每个结点的值都小于或等于其左右孩子结点的值

### Map 

![img](/img/26341ef9fe5caf66ba0b7c40bba264a5_720w.png)

Map 是一种存储键值对映射的容器类，在Map中键可以是任意类型的对象，但不能有重复的键，每个键都对应一个值，真正存储在图中的是键值构成的条目。

#### HashMap

```java
public class HashMap<K,V> extends AbstractMap<K,V>
    implements Map<K,V>, Cloneable, Serializable 
```

HashMap是基于**哈希表**的Map接口的**非同步实现**。在之前的版本中，HashMap采用**数组+链表**实现，即使用链表处理冲突，同一hash值的链表都存储在一个链表里。但是当链表中的元素较多，即hash值相等的元素较多时，通过key值依次查找的效率较低。而JDK1.8中，HashMap采用**数组+链表+红黑树**实现，当链表长度超过阈值（8）时，将链表转换为红黑树（前提是数组桶的长度小于64），这样大大减少了查找时间。

```java
public class HashMap<K,V> extends AbstractMap<K,V> implements Map<K,V>, Cloneable, Serializable {
    // 序列号
    private static final long serialVersionUID = 362498820763181265L;    
    // 默认的初始容量是16
    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4;   
    // 最大容量
    static final int MAXIMUM_CAPACITY = 1 << 30; 
    // 默认的填充因子
    static final float DEFAULT_LOAD_FACTOR = 0.75f;
    // 当桶(bucket)上的结点数大于这个值时会转成红黑树
    static final int TREEIFY_THRESHOLD = 8; 
    // 当桶(bucket)上的结点数小于这个值时树转链表
    static final int UNTREEIFY_THRESHOLD = 6;
    // 桶中结构转化为红黑树对应的table的最小大小
    static final int MIN_TREEIFY_CAPACITY = 64;
    // 存储元素的数组，总是2的幂次倍
    transient Node<k,v>[] table; 
    // 存放具体元素的集
    transient Set<map.entry<k,v>> entrySet;
    // 存放元素的个数，注意这个不等于数组的长度。
    transient int size;
    // 每次扩容和更改map结构的计数器
    transient int modCount;   
    // 临界值 当实际大小(容量*填充因子)超过临界值时，会进行扩容
    int threshold;
    // 填充因子
    final float loadFactor;
}
```

- hash算法

（1）首先获取对象的hashCode()值，然后将hashCode值右移16位，然后将右移后的值与原来的hashCode做**异或**运算，返回结果。（其中h>>>16，在JDK1.8中，优化了高位运算的算法，使用了零扩展，无论正数还是负数，都在高位插入0）。

（2）在putVal源码中，我们通过(n-1)&hash获取该对象的键在hashmap中的位置。（其中hash的值就是（1）中获得的值）其中n表示的是hash桶数组的长度，并且该长度为2的n次方，这样(n-1)&hash就等价于hash%n。因为&运算的效率高于%运算。

* HashMap的put方法

  ![img](/img/58e67eae921e4b431782c07444af824e_720w.png)

  JDK1.7 单链表的采用头插入方式，同一位置上新元素总会被放在链表的头部位置；1.8 是尾插入方式。

- 扩容机制

  当元素数 > 负载因子0.75 * 桶的长度后，hash进行扩容，变成原大小的2倍。JDK1.7之前都是要重新hash运算，1.8后进行了优化。元素的位置要么是在原位置，要么是在原位置再移动2次幂的位置。JDK1.7中rehash的时候，旧链表迁移新链表的时候，如果在新表的数组索引位置相同，则链表元素会倒置。1.8不会。

[JDK1.8 HashMap源码分析]: https://www.cnblogs.com/xiaoxi/p/7233201.html
[Java 8系列之重新认识HashMap]: https://zhuanlan.zhihu.com/p/21673805

#### LinkedHashMap

```java
public class LinkedHashMap<K,V>
    extends HashMap<K,V>
    implements Map<K,V>
```

LinkedHashMap继承自HashMap，它主要是用链表实现来扩展HashMap类，HashMap中条目是没有顺序的，但是在LinkedHashMap中元素既可以按照它们插入图的顺序排序，也可以按它们最后一次被访问的顺序排序, 它额外维护了一个双向链表用于保持迭代顺序。LinkedHashMap可以很好的支持LRU算法。

　	与HashMap相比，LinkedHashMap增加 **双向链表头结点header** ，**双向链表尾结点tail** 和 **标志位accessOrder** (值为true时，表示按照访问顺序迭代；值为false时，表示按照插入顺序迭代)。

​		LinkedHashMap 几乎和 HashMap 一样：从技术上来说，不同的是它定义了一个 Entry<K,V> header，这个 header 不是放在 Table 里，它是额外独立出来的。LinkedHashMap 通过继承 hashMap 中的 Entry<K,V>,并添加两个属性 Entry<K,V> before,after,和 header 结合起来组成一个双向链表，来实现按插入顺序或访问顺序排序。

#### Hashtable

```java
public class Hashtable<K,V>
    extends Dictionary<K,V>
    implements Map<K,V>, Cloneable, java.io.Serializable 
```

默认构造函数，容量为 11，加载因子为 0.75。

* 扩容

  扩容 newCapacity = (oldCapacity << 1) + 1 ，数组中的数据重现哈希。

* put数据

  key或value为空会抛出**NullPointerException**

> HashMap和Hashtable的区别
>
> HashMap是Hashtable的轻量级实现（非线程安全的实现），他们都完成了Map接口。主要的区别有：线程安全性，同步(synchronization)，以及速度。
>
> 1. Hashtable继承自Dictionary类，而HashMap是Java1.2引进的Map interface的一个实现。
>
> 2. HashMap允许将null作为一个entry的key或者value，而Hashtable不允许。
>
> 3. HashMap是非synchronized，而Hashtable是synchronized，这意味着Hashtable是线程安全的，多个线程可以共享一个Hashtable；而如果没有正确的同步的话，多个线程是不能共享HashMap的。Java 5提供了ConcurrentHashMap，它是HashTable的替代，比HashTable的扩展性更好。（在多个线程访问Hashtable时，不需要自己为它的方法实现同步，而HashMap 就必须为之提供外同步(Collections.synchronizedMap)）
>
> 4. 另一个区别是HashMap的迭代器(Iterator)是fail-fast迭代器，而Hashtable的enumerator迭代器不是fail-fast的。所以当有其它线程改变了HashMap的结构（增加或者移除元素），将会抛出ConcurrentModificationException，但迭代器本身的remove()方法移除元素则不会抛出ConcurrentModificationException异常。但这并不是一个一定发生的行为，要看JVM。这条同样也是Enumeration和Iterator的区别。fail-fast机制如果不理解原理，可以查看这篇文章：http://www.cnblogs.com/alexlo/archive/2013/03/14/2959233.html
>
> 5. 由于HashMap非线程安全，在只有一个线程访问的情况下，效率要高于HashTable。
>
> 6. HashMap把Hashtable的contains方法去掉了，改成containsvalue和containsKey。因为contains方法容易让人引起误解。 
>
> 7. Hashtable中hash数组默认大小是11，增加的方式是 old*2+1。HashMap中hash数组的默认大小是16，而且一定是2的指数。
>
> 8. 两者通过hash值散列到hash表的算法不一样：

#### WeakHashMap

```java
public class WeakHashMap<K,V>
    extends AbstractMap<K,V>
    implements Map<K,V> 
```

WeakHashMap是一种改进的HashMap，它对key实行“弱引用”，如果一个key不再被外部所引用，那么该key可以被GC回收。

WeakHashMap类中的Entry 

```java
Entry<K,V> extends WeakReference<Object> implements Map.Entry<K,V> 
```

通过**WeakReference**和**ReferenceQueue**实现的**。 WeakHashMap的key是“弱键”，即是WeakReference类型的；ReferenceQueue是一个队列，它会保存被GC回收的“弱键”。实现步骤是：
  (01) 新建WeakHashMap，将“**键值对**”添加到WeakHashMap中。
      实际上，WeakHashMap是通过数组table保存Entry(键值对)；每一个Entry实际上是一个单向链表，即Entry是键值对链表。
  (02) 当**某“弱键”不再被其它对象引用**，并**被GC回收**时。在GC回收该“弱键”时，**这个“弱键”也同时会被添加到ReferenceQueue(queue)队列**中。
  (03) 当下一次我们需要操作WeakHashMap时，会先同步table和queue。table中保存了全部的键值对，而queue中保存被GC回收的键值对；同步它们，就是**删除table中被GC回收的键值对。

[WeakReference 解析](https://www.bbsmax.com/A/gVdnmoYX5W/)

#### TreeMap

![image-20200328012737054](/img/image-20200328012737054.png)

```java
public class TreeMap<K,V>
    extends AbstractMap<K,V>
    implements NavigableMap<K,V>, Cloneable, java.io.Serializable
```

TreeMap基于**红黑树（Red-Black tree）实现**。该映射根据**其键的自然顺序进行排序**，或者根据**创建映射时提供的 Comparator 进行排序**，具体取决于使用的构造方法。
TreeMap的基本操作 containsKey、get、put 和 remove 的时间复杂度是 log(n) 。
另外，TreeMap是**非同步**的。 它的iterator 方法返回的**迭代器是fail-fastl**的。

Entry 对象保存数据：有key，value，左右节点，父节点，颜色属性。

```java
static final class Entry<K,V> implements Map.Entry<K,V> {
    K key;
    V value;
    Entry<K,V> left;
    Entry<K,V> right;
    Entry<K,V> parent;
    boolean color = BLACK;
```

#### IdentityHashMap

```java
public class IdentityHashMap<K,V>
    extends AbstractMap<K,V>
    implements Map<K,V>, java.io.Serializable, Cloneable
```

IdentityHashMap 利用哈希表实现 Map 接口，比较键（和值）时使用引用相等性代替对象相等性。

- put方法

  1. put的时候先通过引用是否相等判断key是不是已经在表中存在，如果存在更新oldValue为新的value，如果元素个数达到阈值，扩容处理，然后再找合适的位置放置key和value。

  2. 在数组的i索引处存key，而紧挨着i的i+1处存value，并且由于hash方法的原因，key所对应的index全是偶数，自然i+1就是奇数了。这也说明了另一点，数组初始化的时候，数组的长度被定义为默认容量的**2**倍，因为数组元素的每次保存是都占了数组的两个位置。

  3. put的扩容条件是当存放的数组达到数组长度的**1/3**的时候，就需要扩容。

* get方法

  get方法则比较简单，根据key获取数组的索引，然后对象比较引用，基本类型比较数据是否相等即可。如果处找到对象，说明i+1处就是索引对应的value，这也解释了初始化数组的时候2倍长度的原因了。

- 与HashMap的不同
  1. 两者最主要的区别是`IdentityHashMap`使用的是`==`比较key的值，而`HashMap`使用的是`equals()`
  2. `HashMap`使用的是`hashCode()`查找位置，`IdentityHashMap`使用的是`System.identityHashCode(object)`

  3. `IdentityHashMap`理论上来说速度要比`HashMap`快一点

  4. `IdentityHashMap`中key能重复，但需要注意一点的是key比较的方法是`==`，所以若要存放两个相同的key，就需要存放不同的地址。

  5. `IdentityHashMap` 的实现不同于HashMap，虽然也是数组，不过IdentityHashMap中没有用到链表，解决冲突的方式是计算下一个有效索引，并且将数据key和value紧挨着存在map中，即table[i]=key，那么table[i+1]=value。

     

## 多线程

### 线程进程协程

- 进程：每个进程都有独立的代码和数据空间（进程上下文），进程间的切换会有较大的开销，一个进程包含1--n个线程。（进程是资源分配的最小单位）

- 线程：同一类线程共享代码和数据空间，每个线程有独立的运行栈和程序计数器(PC)，线程切换开销小。（线程是cpu调度的最小单位）
- 协程是一种用户态的轻量级线程，协程的调度完全由用户控制。协程拥有自己的寄存器上下文和栈。协程调度切换时，将寄存器上下文和栈保存到其他地方，在切回来的时候，恢复先前保存的寄存器上下文和栈，直接操作栈则基本没有内核切换的开销，可以不加锁的访问全局变量，所以上下文的切换非常快。

### 实现多线程

- 继续*Thread*类
- 实现*Runable*接口.
- 还有一种是实现Callable接口，并与Future、线程池结合使用

### 线程状态转换

![img](/img/20150309140927553.jpeg)

1. 新建状态（New）：新创建了一个线程对象。
2. 就绪状态（Runnable）：线程对象创建后，其他线程调用了该对象的start()方法。该状态的线程位于可运行线程池中，变得可运行，等待获取CPU的使用权。
3. 运行状态（Running）：就绪状态的线程获取了CPU，执行程序代码。
4. 阻塞状态（Blocked）：阻塞状态是线程因为某种原因放弃CPU使用权，暂时停止运行。直到线程进入就绪状态，才有机会转到运行状态。阻塞的情况分三种：
   - 等待阻塞：运行的线程执行wait()方法，JVM会把该线程放入等待池中。(wait会释放持有的锁)
   - 同步阻塞：运行的线程在获取对象的同步锁时，若该同步锁被别的线程占用，则JVM会把该线程放入锁池中。对Running状态的线程加同步锁(Synchronized)使其进入(lock blocked pool ),同步锁被释放进入可运行状态(Runnable)。
   - 其他阻塞：运行的线程执行sleep()或join()方法，或者发出了I/O请求时，JVM会把该线程置为阻塞状态。当sleep()状态超时、join()等待线程终止或者超时、或者I/O处理完毕时，线程重新转入就绪状态。（注意,sleep是不会释放持有的锁）
5. 死亡状态（Dead）：线程执行完了或者因异常退出了run()方法，该线程结束生命周期。

### 线程调度

1. 调整线程优先级：Java线程有优先级，优先级高的线程会获得较多的运行机会。

   Java线程的优先级用整数表示，取值范围是1~10，Thread类有以下三个静态常量：

```java
static int MAX_PRIORITY
          线程可以具有的最高优先级，取值为10。
static int MIN_PRIORITY
          线程可以具有的最低优先级，取值为1。
static int NORM_PRIORITY
          分配给线程的默认优先级，取值为5。
```

​		Thread类的setPriority()和getPriority()方法分别用来设置和获取线程的优先级。
 	   每个线程都有默认的优先级。主线程的默认优先级为Thread.NORM_PRIORITY。
​		线程的优先级有继承关系，比如A线程中创建了B线程，那么B将和A具有相同的优先级。
​		JVM提供了10个线程优先级，但与常见的操作系统都不能很好的映射。如果希望程序能移植到各个操作系统		中，应该仅仅使用Thread类有以下三个静态常量作为优先级，这样能保证同样的优先级采用了同样的调度方		式。

2. 线程睡眠：Thread.sleep(long millis)方法，使线程转到阻塞状态。millis参数设定睡眠的时间，以毫秒为单位。当睡眠结束后，就转为就绪（Runnable）状态。sleep()平台移植性好。
3. 线程等待：Object类中的wait()方法，导致当前的线程等待，直到其他线程调用此对象的 notify() 方法或 notifyAll() 唤醒方法。这个两个唤醒方法也是Object类中的方法，行为等价于调用 wait(0) 一样。
4. 线程让步：Thread.yield() 方法，暂停当前正在执行的线程对象，把执行机会让给相同或者更高优先级的线程。
5. 线程加入：join()方法，等待其他线程终止。在当前线程中调用另一个线程的join()方法，则当前线程转入阻塞状态，直到另一个进程运行结束，当前线程再由阻塞转为就绪状态。
6. 线程唤醒：Object类中的notify()方法，唤醒在此对象监视器上等待的单个线程。如果所有线程都在此对象上等待，则会选择唤醒其中一个线程。选择是任意性的，并在对实现做出决定时发生。线程通过调用其中一个 wait 方法，在对象的监视器上等待。 直到当前的线程放弃此对象上的锁定，才能继续执行被唤醒的线程。被唤醒的线程将以常规方式与在该对象上主动同步的其他所有线程进行竞争；类似的方法还有一个notifyAll()，唤醒在此对象监视器上等待的所有线程。

>  monitor
>
> Java中的每个对象都有一个监视器，来监测并发代码的重入。在非多线程编码时该监视器不发挥作用，反之如果在synchronized 范围内，监视器发挥作用。
>
> wait/notify必须存在于synchronized块中。并且，这三个关键字针对的是同一个监视器（某对象的监视器）。这意味着wait之后，其他线程可以进入同步块执行。
>
> 当某代码并不持有监视器的使用权时去wait或notify，会抛出java.lang.IllegalMonitorStateException。也包括在synchronized块中去调用另一个对象的wait/notify，因为不同对象的监视器不同，同样会抛出此异常。

### 线程同步

1. `synchronized ` 关键字的作用域
   - 是某个对象实例内，synchronized aMethod(){}可以防止多个线程同时访问这个对象的synchronized方法（如果一个对象有多个synchronized方法，只要一个线程访问了其中的一个synchronized方法，其它线程不能同时访问这个对象中任何一个synchronized方法）。这时，不同的对象实例的synchronized方法是不相干扰的。也就是说，其它线程照样可以同时访问相同类的另一个对象实例中的synchronized方法；
   - 是某个类的范围，synchronized static aStaticMethod{}防止多个线程同时访问这个类中的synchronized static 方法。它可以对类的所有对象实例起作用。
2. 除了方法前用synchronized关键字，synchronized关键字还可以用于方法中的某个区块中，表示只对这个区块的资源实行互斥访问。用法是: synchronized(this){/*区块*/}，它的作用域是当前对象；
3. synchronized关键字是不能继承的，也就是说，基类的方法synchronized f(){} 在继承类中并不自动是synchronized f(){}，而是变成了f(){}。继承类需要你显式的指定它的某个方法为synchronized方法；
   

### 多线程高级编程

#### ThreadLocal类

- ThreadLocal是一个本地线程副本变量工具类。每个Thread内部维护着一个ThreadLocalMap，它是一个Map。这个映射表的Key是一个弱引用，其实就是ThreadLocal本身，Value是真正存的线程变量Object。各个线程之间的变量互不干扰，在高并发场景下，可以实现无状态的调用，特别适用于各个线程依赖不同的变量值完成操作的场景。
- 在每个线程Thread内部有一个ThreadLocal.ThreadLocalMap类型的成员变量threadLocals，这个threadLocals就是用来存储实际的变量副本的，键值为当前ThreadLocal变量，value为变量副本（即T类型的变量）。
- 初始时，在Thread里面，threadLocals为空，当通过ThreadLocal变量调用get()方法或者set()方法，就会对Thread类中的threadLocals进行初始化，并且以当前ThreadLocal变量为键值，以ThreadLocal要保存的副本变量为value，存到threadLocals。在当前线程里面，如果要使用副本变量，就可以通过get方法在threadLocals里面查找。
- ThreadLocalMap中解决Hash冲突的方式并非链表的方式，而是采用线性探测的方式，简单的步长加1或减1，寻找下一个相邻的位置。
- 每个ThreadLocal只能保存一个变量副本，如果想要上线一个线程能够保存多个副本以上，就需要创建多个ThreadLocal。
- ThreadLocal内部的ThreadLocalMap键为弱引用，会有内存泄漏的风险。要习惯调用remove方法清除引用。

> ThreadLocal为什么会内存泄漏
>
> ThreadLocal在ThreadLocalMap中是以一个弱引用身份被Entry中的Key引用的，因此如果ThreadLocal没有外部强引用来引用它，那么ThreadLocal会在下次JVM垃圾收集时被回收。这个时候就会出现Entry中Key已经被回收，出现一个null Key的情况，外部读取ThreadLocalMap中的元素是无法通过null Key来找到Value的。因此如果当前线程的生命周期很长，一直存在，那么其内部的ThreadLocalMap对象也一直生存下来，这些null key就存在一条强引用链的关系一直存在：Thread --> ThreadLocalMap-->Entry-->Value，这条强引用链会导致Entry不会回收，Value也不会回收，但Entry中的Key却已经被回收的情况，造成内存泄漏。
>
> 但是JVM团队已经考虑到这样的情况，并做了一些措施来保证ThreadLocal尽量不会内存泄漏：在ThreadLocal的get()、set()、remove()方法调用的时候会清除掉线程ThreadLocalMap中所有Entry中Key为null的Value，并将整个Entry设置为null，利于下次内存回收。
>
> [tomcat多线程处理及ThreadLocal使用注意](https://blog.csdn.net/weixin_42168940/article/details/86626014)
>
> [ThreadLocal-面试必问深度解析](https://www.jianshu.com/p/98b68c97df9b)
>
> [ThreadLocal内存泄漏真因探究](https://www.jianshu.com/p/a1cd61fa22da)



#### 原子类

* 根据操作的数据类型，可以将JUC包中的原子类分为4类

  **基本类型**

  使用原子的方式更新基本类型

  AtomicInteger：整形原子类

  AtomicLong：长整型原子类

  AtomicBoolean ：布尔型原子类

  **数组类型**

  使用原子的方式更新数组里的某个元素

  AtomicIntegerArray：整形数组原子类

  AtomicLongArray：长整形数组原子类

  AtomicReferenceArray ：引用类型数组原子类

  **引用类型**（基本类型原子类只能更新一个变量，如果需要原子更新多个变量，需要使用 引用类型原子类。）

  AtomicReference：引用类型原子类

  AtomicStampedRerence：原子更新引用类型里的字段原子类

  AtomicMarkableReference ：原子更新带有标记位的引用类型

  **对象的属性修改类型**（如果需要原子更新某个类里的某个字段时，需要用到对象的属性修改类型原子类。）

  AtomicIntegerFieldUpdater:原子更新整形字段的更新器

  AtomicLongFieldUpdater：原子更新长整形字段的更新器

  AtomicStampedReference ：原子更新带有版本号的引用类型。该类将整数值与引用关联起来，可用于解决原子的更新数据和数据的版本号，可以解决使用 CAS 进行原子更新时可能出现的 ABA 问题。

* 基本数据类型原子类的优势

  多线程环境下保证线程安全

* 原理

  AtomicInteger 类主要利用 CAS (compare and swap) + volatile 和 native 方法来保证原子操作，从而避免 synchronized 的高开销，执行效率大为提升。

  CAS的原理是拿期望的值和原本的一个值作比较，如果相同则更新成新的值。UnSafe 类的 objectFieldOffset() 方法是一个本地方法，这个方法是用来拿到“原来的值”的内存地址，返回值是 valueOffset。另外 value 是一个volatile变量，在内存中可见，因此 JVM 可以保证任何时刻任何线程总能拿到该变量的最新值。

  > **CAS 介绍**
  >
  > CAS操作（又称为无锁操作）是一种乐观锁策略。
  >
  > ```java
  > public final int getAndAddInt(Object var1, long var2, int var4) {
  >         int var5;
  >         do {
  >             var5 = this.getIntVolatile(var1, var2);
  >         } while(!this.compareAndSwapInt(var1, var2, var5, var5 + var4));
  > 
  >         return var5;
  >     }
  > ```
  >
  >  CAS有3个操作数，内存值V，旧的预期值A，要修改的新值B。当且仅当预期值A和内存值V相同时，将内存值V修改为B，否则什么都不做。可见只有自旋实现更新数据操作之后，while循环才能够结束。
  >
  > 该操作是一个原子操作，被广泛的应用在Java的底层实现中。在Java中，CAS主要是由sun.misc.Unsafe这个类通过JNI调用CPU底层指令实现。

  ## CAS的问题

  1. 自旋时间过长。由`compareAndSwapInt`函数可知，自旋时间过长会对性能是很大的消耗。
  2. ABA问题。因为CAS会检查旧值有没有变化，这里存在这样一个有意思的问题。比如一个旧值A变为了成B，然后再变成A，刚好在做CAS时检查发现旧值并没有变化依然为A，但是实际上的确发生了变化。解决方案可以添加一个版本号可以解决。原来的变化路径A->B->A就变成了1A->2B->3C，或使用AtomicStampedReference工具类。

  ## LongAdder

  为了解决自旋导致的性能问题，JDK8在Atomic包中推出了LongAdder类。LongAdder采用的方法是，共享热点数据分离的计数：将一个数字的值拆分为一个数组。不同线程会命中到数组的不同槽中，各个线程只对自己槽中的那个值进行CAS操作，这样热点就被分散了，冲突的概率就小很多；要得到这个数字的话，就要把这个值加起来。相比AtomicLong，并发量大大提高。

  优点：有很高性能的并发写的能力
  缺点：读取的性能不是很高效，而且如果读取的时候出现并发写的话，结果可能不是正确的

[Java多线程之原子操作类](https://my.oschina.net/u/2425469/blog/3107473#h1_1)

[Java 并发：原子类](https://blog.csdn.net/youyou1543724847/article/details/52735510)

#### Lock类

在java.util.concurrent包内。共有三个实现：

```java
ReentrantLock
ReentrantReadWriteLock.ReadLock
ReentrantReadWriteLock.WriteLock
```

主要目的是和synchronized一样， 两者都是为了解决同步问题，处理资源争端而产生的技术。功能类似但有一些区别。区别如下：

![img](/img/412d294ff5535bbcddc0d979b2a339e6102264.png)

- lock更灵活，可以自由定义多把锁的枷锁解锁顺序（synchronized要按照先加的后解顺序）

- 提供多种加锁方案，lock 阻塞式, trylock 无阻塞式, lockInterruptily 可打断式， 还有trylock的带超时时间版本。

- 可以和Condition接口的结合。

  ```java
  private Condition condition = lock.newCondition();
  ```

  通过lock对象可以获得condition对象。condition接口提供了如下方法：

  ```java
  void await() throws InterruptedException; // 同 ojbect.wait();
  void signal(); // 同 object.notify();
  void signalAll(); // 同 object.notifyall();
  boolean awaitUntil(Date deadline) throws InterruptedException;
  ```

**ReentrantLock**　　　　
可重入的意义在于持有锁的线程可以继续持有，并且要释放对等的次数后才真正释放该锁。

* 使用方法是：

```java
// 1. 先new一个实例 
static ReentrantLock r=new ReentrantLock();
//2. 加锁
r.lock();
// 或 r.lockInterruptibly();
// 或 r.tryLock();

/*此处也是个不同，后者可被打断。当a线程lock后，b线程阻塞，此时如果是lockInterruptibly，那么在调用b.interrupt()之后，b线程退出阻塞，并放弃对资源的争抢，进入catch块。（如果使用后者，必须throw interruptable exception 或catch）　*/

// 3. 释放锁
r.unlock();

/*必须做！何为必须做呢，要放在finally里面。以防止异常跳出了正常流程，导致灾难。这里补充一个小知识点，finally是可以信任的：经过测试，哪怕是发生了OutofMemoryError，finally块中的语句执行也能够得到保证。*/
```

* 实例化方法默认不传参数是非公平锁。

  公平锁：按照线程加锁的顺序来获取锁
  非公平锁：随机竞争来得到锁

*  tryLock

  用来尝试获取锁，如果获取成功，则返回true，如果获取失败（即锁已被其他线程获取），则返回false，也就说这个方法无论如何都会立即返回。在拿不到锁时不会一直在那等待。即使已将此锁设置为使用公平排序策略，但是调用 tryLock() 仍将 立即获取锁（如果有可用的）.

  [Lock，tryLock，lockInterruptibly有什么区别](https://www.zhihu.com/question/36771163)

* 实现原理

  ReentrantLock主要利用CAS+AQS队列来实现。它支持公平锁和非公平锁。

  AbstractQueuedSynchronizer简称AQS。

  ![img](/img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Z1eXV3ZWkyMDE1,size_16,color_FFFFFF,t_70.png)

  AQS使用一个FIFO的队列表示排队等待锁的线程，队列头节点称作“哨兵节点”或者“哑节点”，它不与任何线程关联。其他的节点与等待线程关联，每个节点维护一个等待状态waitStatus

  ReentrantLock的基本实现可以概括为：先通过CAS尝试获取锁。如果此时已经有线程占据了锁，那就加入AQS队列并且被挂起。当锁被释放之后，排在CLH队列队首的线程会被唤醒，然后CAS再次尝试获取锁。在这个时候，如果：

  非公平锁：如果同时还有另一个线程进来尝试获取，那么有可能会让这个线程抢先获取；

  公平锁：如果同时还有另一个线程进来尝试获取，当它发现自己不是在队首的话，就会排到队尾，由队首的线程获取到锁。

  [ReentrantLock原理](https://blog.csdn.net/fuyuwei2015/article/details/83719444)

  [从ReentrantLock的实现看AQS的原理及应用](https://tech.meituan.com/2019/12/05/aqs-theory-and-apply.html)

  [不可不说的Java“锁”事](https://mp.weixin.qq.com/s?__biz=MjM5NjQ5MTI5OA==&mid=2651749434&idx=3&sn=5ffa63ad47fe166f2f1a9f604ed10091&chksm=bd12a5778a652c61509d9e718ab086ff27ad8768586ea9b38c3dcf9e017a8e49bcae3df9bcc8&scene=38#wechat_redirect)

**ReentrantReadWriteLock**

可重入读写锁（读写锁的一个实现），读写锁分成两个锁，一个锁是读锁，一个锁是写锁。两者都有lock,unlock方法。写写，写读互斥；读读不互斥。可以实现并发读的高效线程安全代码。

```java
　ReentrantReadWriteLock lock = new ReentrantReadWriteLock()
　ReadLock r = lock.readLock();
　WriteLock w = lock.writeLock();
  r.lock(); // r.unlock();
	w.lock(); // w.unlock();
```

#### 容器类

* BlockingQueue

  * 放入数据：

    > offer(anObject):表示如果可能的话,将anObject加到BlockingQueue里,即如果BlockingQueue可以容	纳,则返回true,否则返回false.（本方法不阻塞当前执行方法的线程）
    > offer(E o, long timeout, TimeUnit unit),可以设定等待的时间，如果在指定的时间内，还不能往队列	中加入BlockingQueue，则返回失败。
    > put(anObject):把anObject加到BlockingQueue里,如果BlockQueue没有空间,则调用此方法的线程被	阻断直到BlockingQueue里面有空间再继续.

  * 获取数据：

    > poll(time):取走BlockingQueue里排在首位的对象,若不能立即取出,则可以等time参数规定的时间,
    > 　取不到时返回null;
    > poll(long timeout, TimeUnit unit)：从BlockingQueue取出一个队首的对象，如果在指定时间内，
    > 	队列一旦有数据可取，则立即返回队列中的数据。否则知道时间超时还没有数据可取，返回失败。
    > take():取走BlockingQueue里排在首位的对象,若BlockingQueue为空,阻断进入等待状态直到
    > 　BlockingQueue有新的数据被加入; 
    > drainTo():一次性从BlockingQueue获取所有可用的数据对象（还可以指定获取数据的个数）， 
    > 　通过该方法，可以提升获取数据效率；不需要多次分批加锁或释放锁。

  * 常见BlockingQueue

  ![img](/img/2010112416335973.jpg)

  [Java多线程-工具篇-BlockingQueue](https://www.cnblogs.com/jackyuj/archive/2010/11/24/1886553.html)

* ConcurrentHashMap

  **JDK1.5中的实现**

  ConcurrentHashMap使用的是分段锁技术,将ConcurrentHashMap将锁一段一段的存储，然后给每一段数据配一把锁（segment），当一个线程占用一把锁（segment）访问其中一段数据的时候，其他段的数据也能被其它的线程访问，默认分配16个segment。默认比Hashtable效率提高16倍。

  ConcurrentHashMap的结构图如下（网友贡献的图，哈）：

  ![image-20200403184655912](/img/image-20200403184655912.png)

  **JDK1.8中的实现**

  ConcurrentHashMap取消了segment分段锁，而采用CAS和synchronized来保证并发安全。数据结构跟HashMap1.8的结构一样，**数组+链表/红黑二叉树**。
   synchronized只锁定当前链表或红黑二叉树的首节点，这样只要hash不冲突，就不会产生并发，效率又提升N倍。

  JDK1.8的ConcurrentHashMap的结构图如下：

  ![image-20200403184744213](/img/image-20200403184744213.png)

  > **TreeBin:** 红黑二叉树节点
  >  **Node:** 链表节点

JDK8中的实现也是锁分离的思想，它把锁分的比segment（JDK1.5）更细一些，只要hash不冲突，就不会出现并发获得锁的情况。它首先使用无锁操作CAS插入头结点，如果插入失败，说明已经有别的线程插入头结点了，再次循环进行操作。如果头结点已经存在，则通过synchronized获得头结点锁，进行后续的操作。性能比segment分段锁又再次提升。

[ConcurrentHashMap 原理解析](https://www.jianshu.com/p/d10256f0ebea)



#### 管理类

Java通过Executors提供了四种线程池，这四种线程池都是直接或间接配置ThreadPoolExecutor的参数实现的。

##### 可缓存线程池CachedThreadPool()

1. 这种线程池内部没有核心线程，线程的数量是有没限制的。
2. 在创建任务时，若有空闲的线程时则复用空闲的线程，若没有则新建线程。
3. 没有工作的线程（闲置状态）在超过了60S还不做事，就会销毁。

##### FixedThreadPool 定长线程池

该线程池的最大线程数等于核心线程数，所以在默认情况下，该线程池的线程不会因为闲置状态超时而被销毁。

如果当前线程数小于核心线程数，并且也有闲置线程的时候提交了任务，这时也不会去复用之前的闲置线程，会创建新的线程去执行任务。如果当前执行任务数大于了核心线程数，大于的部分就会进入队列等待。等着有闲置的线程来执行这个任务。

##### SingleThreadPool

1. 有且仅有一个工作线程执行任务
2. 所有任务按照指定顺序执行，即遵循队列的入队出队规则

##### ScheduledThreadPool

根据源码可以看出：
 DEFAULT_KEEPALIVE_MILLIS就是默认10L，这里就是10秒。这个线程池有点像是吧CachedThreadPool和FixedThreadPool 结合了一下。

1. 不仅设置了核心线程数，最大线程数也是Integer.MAX_VALUE。
2. 这个线程池是上述4个中为唯一个有延迟执行和周期执行任务的线程池。

[java线程池ThreadPoolExecutor类使用详解](https://www.cnblogs.com/dafanjoy/p/9729358.html)

作者：我弟是个程序员
链接：https://www.jianshu.com/p/ae67972d1156
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

[Java线程池实现原理](https://mp.weixin.qq.com/s/baYuX8aCwQ9PP6k7TDl2Ww)

## 反射

## NIO

## JVM原理

### jvm基本结构

![image](/img/352511-20170810232433792-373676900.png)

class文件被jvm装载以后，经过jvm的内存空间调配，最终是由执行引擎完成class文件的执行。

#### 内存空间

JVM内存空间包含：方法区、java堆、java栈、本地方法栈。

* 方法区

  各个线程共享的区域，存放类信息、常量、静态变量。

* java堆

  java堆也是线程共享的区域，我们的类的实例就放在这个区域，可以想象你的一个系统会产生很多实例，因此java堆的空间也是最大的。如果java堆空间不足了，程序会抛出OutOfMemoryError异常。

* java栈

  java栈是每个线程私有的区域，它的生命周期与线程相同，一个线程对应一个java栈，每执行一个方法就会往栈中压入一个元素，这个元素叫“栈帧”，而栈帧中包括了方法中的局部变量、用于存放中间状态值的操作栈。如果java栈空间不足了，程序会抛出StackOverflowError异常，想一想什么情况下会容易产生这个错误，对，递归，递归如果深度很深，就会执行大量的方法，方法越多java栈的占用空间越大。

* 本地方法栈

  本地方法栈角色和java栈类似，只不过它是用来表示执行本地方法的，本地方法栈存放的方法调用本地方法接口，最终调用本地方法库，实现与操作系统、硬件交互的目的。

