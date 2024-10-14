---
title: '[Java Training]Week 6'
date: 2020-04-21 21:21:37
categories: Java
tags: Java
index_img: https://i.loli.net/2019/07/07/5d21cd23675da29020.jpg
---

# 0x00

​    本系列-Java集训系列

​    变成了自己学习一遍Java- -。

# 0x01

​    第七章 异常、断言和日志

# 0x02

## 异常

1. 程序总会产生错误，如果是在开发阶段，那么还可以看到错误去修复，然后重新启动，但是在程序的运行阶段，就不可以这样，所以当错误产生的时候，至少做到以下几点：
   - 向用户通告错误
   - 保存所有的工作结果
   - 允许用户以妥善的形式退出程序

2. 将程序可能产生的错误做一个归类
   - 用户输入错误：用户不可能总是按照软件开发者的预期进行输入，会经常产生各种奇怪的输入，程序如果没有进行检查，那么就会产生错误
   - 设备错误：硬件可能在你发出指令之后不会正常执行，比如没有接上打印机，比如打印机没纸了
   - 物理限制：磁盘满了
   - 代码错误：代码无法正确执行，比如调用了错误的方法，方法返回的是null，然后对null进行了方法调用等

3. 不论是系统还是语言，都会有一个异常处理机制，以便程序返回一种安全状态，并能够让用户执行一些其他的命令；或者允许用户保存所有操作的结果，并以妥善的方式终止程序

4. 异常分类

   - 分类如下图

   ![Java异常层次结构](https://i.loli.net/2020/04/26/6UnZCvREc7SPJAk.png)

   - 所有的异常都是由Throwable继承而来，下一层分解为Error和Exception

   - Error类层次结构描述了Java运行时系统的内部错误和资源耗尽错误

   - Exception类下属两个分支，RuntimeException是由程序错误导致的异常；IOException是程序本身没有问题，但由于像I/O错误等这类问题导致的异常属于其他异常

   - 重点关注的是Exception，而Error应该尽量避免，也无法处理Error的错误

   - Exception中，派生于RuntimeException的异常包括以下几种情况：

     1. 错误的类型转换
     2. 数组访问越界
     3. 访问null指针

   - 不是派生于RuntimeException的异常包括：

     1. 试图在文件尾部后面读取数据
     2. 试图打开一个不存在的文件
     3. 试图根据给定的字符串查找Class对象，而这个字符串表示的类并不存在

   - 派生于Error类或RuntimeException类的所有异常成为<b>非受查异常</b>，IOException在内的所有其他异常成为<b>受查异常</b>，其中受查异常是需要处理的，即抛出、捕获等

     想必看完上面已经看懵了，这里我用我自己粗浅的理解解释一下，简单说呢，非受查异常（Error和RuntimeException）是外界原因或者代码原因，Error不可控，没办法检查；RuntimeException是可控，最好的办法就是通过代码限制来规避，不需要检查。所以剩下的就是受查异常（IOException）

5. 声明受查异常。

   * 方法应该在其首部生命所有可能抛出的异常。下面是一个例子

     > public FileInputStream(String name) throws FileNotFoundException

   * 自己编写方法时，不必将所有可能抛出的异常都进行声明。以下四种情况需要抛出异常：

     1. 调用一个抛出受查异常的方法，例如，FileInputStream构造器。

     2. 程序运行过程中发现错误，并且利用throw语句抛出一个受查异常。

     3. 程序出现错误，例如，a[-1]=0会抛出一个ArrayIndexOutOfBoundsException这样的非受查异常。

     4. Java虚拟机和运行时库出现的内部错误。

        如果出现前两种情况，则必须告诉调用这个方法的程序员有可能抛出异常。

   * 对于那些可能被他人使用的Java方法，应该根据异常规范，在方法的首部声明这个方法可能抛出的异常

     ```java
     class MyAnimation
     {
         //....
         public Image loadIeg(String s) throws IOException
         {
          //....   
         }
     }
     ```

     如果抛出多个异常，那么就用逗号分隔

     ```java
     class MyAnimation
     {
         //....
         public Image loadImage(String s) throws FileNotFoundException,EOFException
         {
             //....
         }
     }
     ```

   * 声明的应该都是受查异常，非受查异常不应该声明。所以，也不应该声明从RuntimeException类派生的异常，而是应该在代码上阻止产生RuntimeException异常。

6. 也可以在逻辑有错误的时候主动抛出异常，抛出方法

   ```java
   throw new EOFException();
   ```

   例：

   ```java
   String readData(Scanner in) throws EOFException
   {
       while(True)
       {
           if (!in.hasNext()) // EOF encountered
           {
               if (n < len)
                   throw new EOFException();
           }
       }
       retrn s;
   }
   ```

7. 根据上一点，发现抛出已存在的异常很轻松：

   * 找到一个合适的异常类
   * 创建这个类的一个对象
   * 将对象抛出

8. 创建自己的异常类：

   ```java
   class FileFormatException extends IOException
   {
       public FileFormatException() {}
       public FileFormatException(String gripe)
       {
           super(gride);
       }
   }
   ```

   很多时候需要抛出一些自定义异常，来准确的描述发生的情况

   首先是一定要继承一个Exception类，然后要有默认构造方法和一个带详细描述参数的构造方法，其他方法视情况添加

   抛出自定义异常的方法并没有区别

   ```java
   String readData(BufferedReader in) thros FileFormatException
   {
       while(true)
       {
           if (ch == -1) // EOF encountered
           {
               if (n < len)
               {
                   throw new FileFormatException();
               }
           }
       }
   }
   ```

9. 抛出异常只是把异常的处理交给调用者，并没有真正的处理。如果不进行捕获（处理），程序就会终止运行。捕获异常之后，就可以在代码块中处理异常。

   捕获异常的代码：

   ```java
   try
   {
       // code
       // 需要捕获的异常的代码
   }
   catch(ExceptionType e) //
   {
       // code
       // 如何处理捕获到的异常
}
   ```
   
   会抛出异常的代码在 try 代码块中，当try中的代码触发异常，并且抛出的异常的类型在 catch 中有，则直接进入 catch 中对应的代码块进行执行。
   
   如果没有触发异常，则跳过 catch 中的代码。
   
   示例代码
   
   ```java
   public void read(String filename)
   {
       try
       {
           InputStream in = new FileInputStream(filename);
           int b;
           while ((b = in.read()) ! = -1)
           {
               // process input
           }
       }
       catch (IOException exception)
       {
           exception.printStackTrace();
       }
   }
   ```
   
   可以在一个try中捕获多种异常，catch的方式类似于ifelse
   
   ```java
   try
   {
       // 受查异常的代码
   }
   catch (FileNotFoundException e)
   {
       // 处理代码
   }
   catch (UnknownHostException e)
   {
       // 处理代码
   }
   catch (IOException e)
   {
       // 处理代码
   }
   ```
   
   获取异常的信息
   
   > e.getMessage()
   
   或者更详细的
   
   > e.getClass().getName()
   
   也可以在同一个catch中匹配多个不同的异常类型
   
   ```java
   try
   {
       // code
   }
   catch (FileNotFoundException | UnknownHostException e)
   {
       // code
   }
   catch (IOException e)
   {
       // code
   }
   ```
   
10. 在异常中抛出另一种异常，即改变异常类型，可以在catch中重新抛出另一个异常

    ```java
    try
    {
        // code
    }
    catch (SQLException e)
    {
        Throwable se = new ServletException("database error");
        se.initCause(e);
        throw se;
    }
    ```

    这样既不丢失原始信息，还可以随意定义异常，想看原始信息通过以下方法

    > Throwable e = se.getCause();

    

11. 保证不论是否触发异常都会执行的代码块，finally，

    ```java
    InputStream in = new FileInputStream();
    try
    {
        // code
    }
    catch (IOException e)
    {
        // code
    }
    finally
    {
        in.close();
    }
    ```

    上面这段代码中，不论怎么样都会执行finally中的 in.close()

12. 如果想要只是关闭资源链接，那么可以用带资源的try语句

    ```java
    try(Scanner in = new Scanner(new FileInputStream("/usr/share/dict/words"), "UTF-8");
       PrintWriter out = new PrintWriter("out.txt"))
    {
        while(in.hasNext())
            out.println(in.next().toUpperCase());
    }
    ```

    如上代码不论怎么样都会关闭in和out，如果需要关闭资源，那么尽量用这种方式

13. 当产生异常的时候，需要分析产生原因，这时候可以使用分析堆栈的方法

    可以调用Throwable类的printStackTrace方法

    ```java
Throwable t = new Throwable();
    StringWriter out = new StringWriter();
t.printStackTrace(new PrintWriter(out));
    String description = out.toString();
    ```

    

还有更灵活的 使用getStackTrace方法，会得到StackTraceElement对象的数组
    
​```java
    Throwable t = new Throwable();
StackTraceElement[] frames = t.getStackTrace();
    for (StackTraceElement frame : frames)
    // code
```

    静态的Thread.getAllStackTrace方法，可以产生所有线程的堆栈轨迹
    
    ```java
Map<Thread, StackTraceElement[]> map = Thread.getAllStackTraces();
    for (Thread t : map.keySet())
{
        StackTraceElement[] frames = map.get(t);
    // code
    }

```

14. 使用异常的一些技巧

    * 异常处理不能代替简单的测试
    * 不要过分的细化异常
    * 利用异常层次结构
    * 不要压制异常
    * 在检测错误时，苛刻要比放任更好

## 断言

1. 断言的关键字时assert

2. 断言是对一个条件进行判断，如果不通过（即为false），则抛出一个AssertionError异常

3. 断言有如下两种形式

   > assert 条件;

   或

   > assert 条件 : 表达式;

4. 断言是被用来在开发的时候进行测试的，默认情况下是不启用的，放在代码里也不会对速度产生影响，在运行程序时用 -enableassertions 或 -ea 选项启用断言

   > java -enableassertions MyApp

   或

   > java -ea MyApp

   也可以在某个类或整个包中使用断言

   > java -ea:MyClass -ea:com.mycompany.mylib... MyApp

   启用断言不需要重新编译程序

5. 关于断言需要注意的点

   * 断言失败是致命的、不可恢复的错误
   * 断言检查只用于开发和测试阶段

6. 断言使用示例

   ```java
   // 当i小于0的时候，就会报错并且退出程序
   assert i >= 0;
   ```


## 日志

1. 日志的意义：初学者会发现调试神器 System.out.println() ，但是每次都要在调试地点插入这句话，然后在调试完成之后再注释掉或者删除，这样是十分不优雅的，日志就是一个十分优雅的解决方案

   * 可以很容易地取消全部日志记录，或者仅仅取消某个级别的日志，而且打开和关闭这个操作也很容易
   * 可以很简单的禁止日志记录的输出，因此，将这些日志代码留在程序中的开销很小
   * 日志记录可以被定向到不同的处理器，用于再控制台中显示，用于存储在文件中等
   * 日志记录器和处理器都可以对记录进行过滤。过滤器可以根据过滤实现器制定的标准丢弃那些无用的记录项
   * 日志记录可以采用不同的方式格式化，例如，纯文本或XML
   * 应用程序可以使用多个日志记录器，它们使用类似包名的这种具有层次结构的名字，例如，com.mycompany.myapp
   * 在默认情况下，日志系统的配置由配置文件控制。如果需要的话，应用程序可以替换这个配置

2. 最简单的日志使用方法

   使用全局日志记录器（global logger）并调用其info方法：

   ```java
   Logger.getGlobal().info("File->Open menu item selected");
   ```
```

   在默认情况下，这条记录将会显示以下内容

   > May 10, 2013 10:12:15 PM LoggingImageViewer fileOpen
   >
   > INFO: File->Open menu item selected

   但是，如果在适当的地方（如main开始）调用

   ```java
   Logger.getGlobal().setLevel(Level.OFF);
```

   会取消所有的日志

3. 高级使用日志方法

   可以自定义日志记录器，而不是所有都用全局日志记录器

   ```java
   private static final Logger myLogger = Logger.getLogger("com.mycompany.myapp");
   ```

   与包名类似，日志记录器名字也有层次结构，而且日志记录器还可以继承设置，比如com.mycompany 设置的级别是FINE，那么子包都会默认级别是FINE，如 com.mmycompany.abc
   
4. 通常有以下日志记录器级别：

   * SEVERE
   * WARNING
   * INFO
   * CONFIG
   * FINE
   * FINER
   * FINEST

   默认情况下只记录前三个级别，也可以手动设置级别：

   ```java
   // 在日志记录之前加上这行代码，就成功将日志级别改成FINE
   logger.setLevel(Level.FINE);
   ```

   这样在日志中就记录FINE以上的级别的日志

5. 记录不同级别的日志

   ```java
   logger.warning(message);
   logger.fine(message);
   logger.log(Level.FINE, message);
   ```

6. 跟踪调用的方法

   ```java
   // 获得调用类和方法的确切位置的方法
   void logp(Level l, String className, String methodName, String message)
   //跟踪执行流的方法
   void entering(String className, String methodName)
   void entering(String className, String methodName, Object param)
   void entering(String className, String methodName, Object[] params)
   void exiting(String className, String methodName)
   void exiting(String className, String methodName, Object result)
   ```

   例子：

   ```java
   int read(String file, String pattern)
   {
       logger.entering("com.mycompany.mylib.Reader", "read", new Object[] {file, pattern});
       // code
       logger.exiting("com.mycompany.mylib.Reader", "read", count);
       return count;
   }
   ```

7. 在代码中进行配置不容易更改，也不容易复用。更好的解决方案是使用配置文件。

