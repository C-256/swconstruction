---
title: Java学习 Day 1~2
published: true
---

# 在学习Java之前

我在学习Java之前，有接触过若干编程语言，例如C#（我接触的第一门语言）、C、C++、Python，以及用于前端开发的JavaScript。在此之前已经对面向对象和泛型有了一定的理解。对Java基础的学习更侧重于其语法和独有的特性

# Java的基本特点

## Java是一门运行在虚拟机上的语言

和C#类似，Java的代码是运行在虚拟机上的，也就是需要JVM的支持才能运行。类似于C#使用.Net Framework。Java在虚拟机运行上这一点确保了Java是一门完全面向对象的语言（因为JVM会保证类的私有成员不会在程序执行的过程中被访问，但是C++中的指针可以越过`private`关键字的限制而访问到私有成员，破坏了面向对象基本特征中的封装性。）

## Java是一门安全的语言

和C#类似，Java是一门安全的语言（当然是和C、C++相对的）。C/C++的指针虽然具有一定的灵活性，但是指针也会在很多的情况下造成麻烦。此外，C/C++的设计初衷是“信任程序员”的，对很多未定义行为没有严格的检查，甚至连一个Warning也不会报错。例如数组越界的问题。此外，由于这两门语言允许程序员直接操作底层的内存，可能导致用户使用时常常出现内存泄露。和这些语言相比，Java删除了指针的语法，引入了垃圾回收机制，增大了其安全性。

## Java的语言“特性”是按包组织的

Java的很多“特性”，甚至是“组成成分”，都是按包来组织的。需要在文件的开头处`import`，而不像C/C++那样使用`#include`预处理指令，也不像C#那样使用`using`

# Java的基本语法

## 输入输出语句：

Java的基本输出语句为：

```java
System.out.println(...);  // 输出并换行
System.out.print(...);    // 输出但不换行
System.out.printf(...);   // 格式化输出，和C类似
```

Java的基本输入语句比其它语言麻烦很多，为

```java
import java.util.Scanner;             // Java的输入需要依靠Scanner类

Scanner in = new Scanner(System.in);
in.nextLine();                        // 获取下一行，返回值为string
in.nextInt();                         // 获取下一个整数
in.nextDouble();                      // ...
```

## 基本数据类型

1. 整数型

Java支持四种大小的整数型，而且它们的大小是被语言所限制的（和C++不同，C++的`int`大小是不确定的，它可能是32位，但是也有可能是16位的），这些类型的大小如下表

| 类型 | 位数 |
| :-: | :-: |
| `byte` | 8 |
| `short` | 16 |
| `int` | 32 |
| `long` | 64 |

除了上表所示的四种以外，还有大整数类型`BigInteger`，可以用来表示很大的整数，但是Java不像C++和C#那样支持运算符重载，所以需要使用`add()`之类的方法来实现运算、比较大小，大整数类型的输入和输出也需要使用专门的函数。大整数类型实际上是一种引用类型，要防止`null`

大整数在`java.math.BigInteger`类，使用前需`import`。

2. 小数型

Java支持单精度浮点数和双精度浮点数两种浮点小数。

| 类别 | 类型 | 位数 |
| :-: | :-: | :-: |
| 单精度浮点数 | `float` | 32 |
| 双精度浮点数 | `double` | 64 |

此外还有大十进制数`BigDecimal`，和大整数类似，它也是一个引用类型。由于二进制下很多的小数都无法使用有限小数表示，`float`和`double`类型都有一定的精度丢失，例如`double`类型的0.3可能和实际的0.3相差一个很小的小数，但是这也确实导致了精度的丢失，可能会出现以下情况

```java
double a = 0.3
System.out.println(a == 0.3 ? "Equals" : "Not Equals");
```

输出为：

```
Not Equals
```

出于相同的原因，不要使用`BigDecimal BigDecimal(double a_double_var);`，如果想从一个`double`变量为一个大十进制数赋值，可以使用`static BigDecimal valueOf(double a_double_var);`。当然也可以使用一个字符串来初始化一个大十进制数。

大十进制数在`java.math.BigDecimal`类，使用前需`import`。

# 一些心得体会

~~为什么没有运算符重载！！！~~
