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

### Queue

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



## 多线程

## NIO



