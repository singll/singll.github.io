---
title: '[Java Training]Week 2'
date: 2019-07-13 09:16:50
categories: Java
tags: Java
index_img: https://i.loli.net/2019/07/07/5d21cd23675da29020.jpg
---
# 0x00
    本系列-Java集训系列
    记录我带领小组进行Java学习，按照《Java核心技术》第十版进行学习
# 0x01
    从第三章开始内容变多，每次基本就一章
## 第三章

 > HelloWorld.java

```java
//HelloWorld类，注意大小写，类名与文件名一致
public class HelloWorld {
    //main方法，作为程序入口，格式基本固定，void是方法的返回类型，这里void是没有返回的意思
    public static void main(String[] args)
    {
        //向控制台输出的方法，调用，传参Hello World ，运行程序将输出 Hello World
        System.out.println("Hello World");
        //单行注释，只能注释掉这一行的

        /*
          多行注释，可以在里面随便写，注意不能在这里嵌套另一个多行注释
        */

        /**
         *这也是注释，用于文档的注释，IDE中可以自动生成
         */
    }
}
```

  先从第一个HelloWorld程序开始
1. Java区分大小写
2. 文件名和类名一致，一般一个<b>.java</b>文件里只有一个类，如果有多个类，其他的类可以不需要与文件名同名（类名不可以重复），并且不能用<b>public</b>修饰类
3. 类名的命名规则：名字必须以字母开头，后面可以跟字母和数字的任意组合，经测试可以使用下划线，名字长度无限制，不能使用<b>Java保留字</b> 
4. 如果需要运行，则需要一个<b>main</b>方法，此方法为程序的入口点
5. 类、方法、属性，都是有访问控制符，有<b>public</b>、<b>protected</b>、<b>private</b>三种，后续章节会详细介绍
6. {}里的是代码段，Java中的任何方法的代码都要用"{"开始，用"}"结束，类也是如此
7. main里的代码作用是在控制台进行输出，调用的<b>println</b>方法，此方法位于<b>System.out</b>对象，调用对象的方法用<b>.</b>，方法可以传参，也可以不传参，但是一定要由<b>()</b>，里面的<b>"Hello World"</b>就是传进去的参数，如果是多个参数，就用<b>,</b>分隔，比如<b>("Hello","World")</b>
8. 双斜线<b>//</b>后面的是注释，//后面的都会被忽略，Java一共由三种注释，//、/* */、/** */，都在代码中可以看到用法

规则讲完，以下是运行此代码的方法：
1. 首先进入<b>命令行</>，进入java文件所在的目录（注：命令行在Windows下进入方式:<b>win</b>+<b>r</b>，输入<b>cmd</b>，点击确认；进入java文件所在目录：<b>cd xxxx</b>，xxxx是java文件所在的目录，注意中间有个空格）
2. 输入命令<b>javac HelloWorld.java</b>，运行，会在本文件夹下生成一个HelloWOrld.class文件，如果报错请查看jdk安装是否正确，java文件是否正确
3. 输入命令<b>java HelloWorld</b>，运行，会看到输出结果，注意这里是<b>HelloWorld</b>，而不是<b>HelloWorld.class</b>

> DataType.java
```java
public class DataType {
    public static void main(String[] args)
    {
        // 整型，分四种，分别为 int 、 short 、 long 、 byte
        // int，整型，占4个字节，取值范围：-2,147,483,648    +2,147,483,647
        int intPrice0;
        intPrice0 = 2147483647;
        int intPrice1 = -2_147_483_648;

        // short，整型，占2个字节，取值范围：-32 768        +32 767
        short shortPrice0;
        shortPrice0 = 32767;
        short shortPrice1 = -32_768;

        // long，整型，占8个字节，取值范围：-9 223 372 036 854 775 808    +9 223 372 036 854 775 807
        long longPrice0;
        longPrice0 = 9223372036854775807L; // 注意，必须在数字后面加一个字母L或小写l，不然会被识别为int类型
        long longPrice1 = -9_223_372_036_854_775_808l;

        // byte，整型，占1个字节，取值范围：-128       +127
        byte bytePrice0;
        bytePrice0 = 127;
        byte bytePrice1 = -128;

        // 还可以使用二进制、八进制、十六进制赋值
        int intPrice2 = 0b1001; // 二进制赋值，可以使用0b或者0B前缀来表示
        System.out.print("intPrice2=");
        System.out.println(intPrice2); // 输出：9

        int intPrice3 = 010; // 八进制赋值，以0开头，容易混淆，谨慎使用
        System.out.print("intPrice3=");
        System.out.println(intPrice3); // 输出：8

        int intPrice4 = 0xCAEF; // 十六进制赋值，可以使用0x或者0X前缀来表示
        System.out.print("intPrice4=");
        System.out.println(intPrice4); // 输出：51951



        // 浮点类型，两种，float 、 double
        // float，浮点数，占4个字节，取值范围 大约 -3.402 823 47 * 10的38次方    +3.402 823 47 * 10的38次方 用科学计数法表示为 大约正负 3.402 823 47E38F
        float floatPrice0;
        floatPrice0 = 3.14F; // 注意，必须在数字后面加F或f，不然会被识别为double
        float floatPrice1 = -3.14f;

        // double,浮点数，占8个字节，取值范围 大约 -1.797 693 134 862 315 70 * 10的308次方    +1.797 693 134 862 315 70 * 10的308次方 用科学计数法表示为 大约正负 1.797 693 134 862 315 70E308
        double doublePrice0;
        doublePrice0 = 3.14; // double可以不加后缀，也可以在数字后面加D或d
        double doublePrice1 = -3.14D;

        // 浮点数有三个特殊的浮点数值，正无穷大、负无穷大、NAN（不是一个数字）
        // 例子
        double doublePrice2 = 33/0.0; // 注意除数不能写成0，会报错
        System.out.print("（正无穷）doublePrice2 = ");
        System.out.println(doublePrice2); // 输出：Infinity

        double doublePrice3 = (-33)/0.0; // 注意除数不能写成0，会报错
        System.out.print("（负无穷）doublePrice3 = ");
        System.out.println(doublePrice3); // 输出：-Infinity

        double doublePrice4 = 0/0.0; // 注意除数不能写成0，会报错
        System.out.print("（NaN）doublePrice4 = ");
        System.out.println(doublePrice4); // 输出：NaN

        // 如果需要判断是否是特殊数值，请用方法来判断
        System.out.println("doublePrice4 is NaN ? " + Double.isNaN(doublePrice4));
        // 如果用 == 来判断，会出现错误的结果
        System.out.println("(Mistake)doublePrice4 is NaN ？" + (doublePrice4 == Double.NaN)); // 判断永远为false，与书上写的不一致，以实践结果为准



        // char类型
        char charTest0 = 'A';
        System.out.println("charTest0 is "+ charTest0);
        char charTest1 = '\u03C0';
        System.out.println("charTest1 is " + charTest1);
        // 注：char类型应用场景很少，正常建议使用String类型



        // boolean类型
        boolean booleanValue0 = true;
        boolean booleanValue1 = false;
        // 注，boolean只有这两个值，表示真和假



        // 变量与常量
        // 上面广泛使用的就是变量的定义
        int i; // 声明变量i为int类型
        i = 1; // 将i赋值为1
        int a = 2; // 也可以在声明的同时直接初始化为某个值
        int j,k,n,m; // 也可以同时声明多个变量，用逗号，分隔

        final int CONT_INT_PRICE = 30; // 常量用final 修饰，惯例是变量名大写，便于与变量区分
        // CONT_INT_PRICE = 23; // 对常量的值进行修改会报错
        final int CONT_INT_PP;
        CONT_INT_PP = 25; // 可以先声明，再赋值
        // CONT_INT_PP = 55; // 赋值过之后再更改就会报错，即如果声明的同时没有初始化，第一次赋值的时候是合法的，第二次修改就会报错
    }
}

```

Java共有8种基本类型，包括：4种整型（int,short,long,byte）、2种浮点类型（float,double）、1种char类型（char）、1种boolean类型（boolean）
1. String不属于基本类型
2. 数据类型和变量常量的规则详见代码注释


> Operator.java

```java
public class Operator {
    public static void main(String[] args)
    {
        // 基本算术运算符 +、-、*、/ 即，加减乘除，以及求余 %
        // 按照书里说，由于Java的跨平台性，会保证在所有机器上运算结果一致
        int a = 5;
        int b = 2;
        System.out.println("5 + 2 = " + (a + b) );
        System.out.println("5 - 2 = " + (a - b));
        System.out.println("5 * 2 = " + (a * b));
        System.out.println("5 / 2 = " + (a / b) );
        System.out.println("5 % 2 = " + (a % b));

        // 一个数学运算库Math类
        double x = 4;
        double y = Math.sqrt(x); // 计算x的平方根，赋给y
        System.out.println(y); // 输出：2.0

        double y2 = Math.pow(x, 3); // 计算x的3次幂，赋给y2
        System.out.println(y2); // 输出：64.0
        // Math类还有好多方法，就不一一列举了，具体的可以参考Java手册

    }
}
```

四则运算这些没什么好说的，看代码就好。

> TypeConversion.java

```java
public class TypeConversion {
    public static void main(String[] args)
    {
        // 隐式类型转换，从int转float可能会丢失精度，即如果int的位数比float能表示的位数大，则会丢失精度
        int n = 123456789;
        float f = n;
        System.out.println(f); // 输出：1.23456792E8

        // 不同数值类型间进行四则运算会先进行转换，将其中的一个类型转成另一个类型，再进行计算
        // 转换优先级为 double->float->long->int，即如果其中有一个double类型，则另一个数字转成double再进行计算，之所以是这种优先级，是因为从位数少的类型转到类型高的类型不会丢失精度
        System.out.println(n+f); // 输出：2.46913584E8
        
        // 强制类型转换
        // 从double到int会进行截断，直接从小数位截，不会进行四舍五入
        double x = 9.997;
        int nx = (int)x;
        System.out.println(nx); // 输出：9

        // 进行舍入操作要用Math的方法
        int nx2 = (int)Math.round(x); // 由于round返回类型是long，所以此处需要强制类型转换
        System.out.println(nx2); // 输出：10
        
        
    }
}
```


1. 关于两个不同类型进行四则运算
    1. 如果两个操作数中有一个是double类型，另一个操作数就会转换为double类型
    2. 否则，如果其中一个操作数是float类型，另一个操作数将会转换为float类型
    3. 否则，如果其中一个操作数是long类型，另一个操作数将会转换为long类型
    4. 否则，两个操作数都将被转换为int类型
2. 关于数值类型之间的合法转换
    1. byte -> short
    2. short -> int
    3. char -> int
    4. int -> long
    5. int -> double
    6. float -> double
    7. int ~> float (此符号表示会丢失精度)
    8. long ~> float 
    9. long ~> double
3. 如果转换前的类型比转换后的类型大很多，就会造成转换之后的数字和转换之前的完全不同，比如(byte)300 = 44，以二进制进行截断，而不是以十进制进行截断

> Operator2.java

```java
public class Operator2 {
    public static void main(String[] args)
    {
        // 赋值与运算符结合，得到简略形式
        int x = 1;
        x += 4; // += 运算符表达的意义为 x = x + 4
        // x = x + 4; // 即上面的完整形式
        // 更多的类似运算符 += 、 -= 、 *= 、/= 、 %=
        x /= 4;

        // 自增自减运算符
        x++; // 即 x = x + 1;
        x--; // 即 x = x - 1;

        // 比较运算符
        boolean b_1 = (3 == 7); // == 用来检测两个数字、变量或对象的相等性，返回boolean值，注意：用 == 来判断两个对象只会判断是否是同一对象
        boolean b_2 = (3 != 7); // != 用来检测不等性，正好与上面相反，用法一样
        // 其他通常用于比较数值的还有 大于 > 、小于 < 、 大于等于 >= 、 小于等于 <=
        // 举个栗子
        boolean b_3 = (3 <= 7);

        // 逻辑运算符 与或非 && || !
        // 其中与、或 是需要两个返回值为boolean的表达式，非 只需要一个
        boolean b_4 = (x != 0) && (x > 0); // 与 逻辑运算符，当两个表达式的结果都为true（真）的时候，b_4 为 true，其余情况为false。此值为真
        boolean b_5 = (x == 0) || (x < 0); // 或 逻辑运算符，当两个表达式结果都为false（假）的时候，b_5为false，其余情况为true，此值为假
        // && 与 || 都存在短路操作，即，如果在获得符号前面部分表达式的结果，就能得到整个表达式的结果，将不会运行符号后面的表达式
        // 栗子： (x == 0) && (x > 0)  ;由于&&符号的特性，在(x == 0)为假的情况下，整个表达式返回结果必然为假，所以后面的( x > 0)不会运行（注意是不会运行）
        // 再来个栗子： (x != 0) || (x < 0)    ;由于||符号的特性，再(x != 0)为真的情况下，整个表达式返回结果必然为假，所以后面的(x < 0)不会运行
        boolean b_6 = !(x == 0);           // 非 逻辑运算符，当表达式为真，返回结果为假，当表达式结果为假，返回结果为真，即将表达式的boolean值反转一下

        // 三元操作符 ?:
        String result = (x != 0)? "aaa" :"bbb"; // 问号之前的表达式必须返回值为boolean，然后如果为true，则执行问号和冒号中间的语句，如果为false，则执行冒号后面的语句
        System.out.println(result); // 输出：aaa
        // (x != 0)?System.out.println("aaa"):System.out.println("bbb");
        // 注：上面注释里这句会被识别成错误，编译不通过，要将整个三元表达式赋值给一个变量，不清楚是不是由于IDE

        // 位运算符& | ^ ~   ，位与  位或 位异或 位非
        // 与逻辑运算符差不多，不过是针对位来进行的运算，多了个异或，异或是在两个条件同时为真或同时为假的时候，结果为假，不同时为真
        byte n = 127;
        int fourthBitFromRight = (n & 0b1000); // 0b1111 & 0b1000 = 0b1000; 换算成10进制为8
        System.out.println(fourthBitFromRight); // 输出：8

        // 左移 <<  右移 >> 以0填充的 右移 >>>
        int intUse0 = 8; // 0b 0000 0000 0000 0000 0000 0000 0000 1000
        int intUse1 = (intUse0 >> 2); // 0b 0000 0000 0000 0000 0000 0000 0000 0010 ,所有位向右移2位，左侧以符号位填充，正数的符号位为0，所以填充0
        System.out.print("intUse0 的二进制：");
        System.out.println(Integer.toBinaryString(intUse0)); // 输出：1000
        System.out.print("intUse1 的二进制：");
        System.out.println(Integer.toBinaryString(intUse1)); // 输出：10


        // 注，负数采用补码方式，所以负数是反着来的
        int intUse2 = -128; // 0b 1111 1111 1111 1111 1111 1111 1000 0000   注意，左边的第一位是符号位，负数为1，正数为0
        int intUse3 = (intUse2 >> 3); // 0b 1111 1111 1111 1111 1111 1111 1111 0000 整体向右移三位，并且以符号位填充
        System.out.print("intUse2 的二进制：");
        System.out.println(Integer.toBinaryString(intUse2)); // 输出：11111111111111111111111110000000
        System.out.print("intUse3 的二进制：");
        System.out.println(Integer.toBinaryString(intUse3)); // 输出：11111111111111111111111111110000

        int intUse4 = (intUse2 >>> 3); //0b 0001 1111 1111 1111 1111 1111 1111 0000 整体向右移三位，符号位以0填充
        System.out.println(intUse4);
        System.out.print("intUse4 的二进制：");
        System.out.println(Integer.toBinaryString(intUse4)); // 输出：11111111111111111111111110000



        // 运算符的优先级，这里只举个栗子，具体的看《运算符优先级》表，平常就使用（）就好，一般不要依赖优先级，首先不容易调试，其次看起来也很乱
        int a1, b1, c1;
        a1 = 3;
        b1 = 5;
        c1 = 7;
        a1 += b1 += c1; // 因为同属同一个操作符，并且此操作符是从右向左，所以先计算 b1+=c1 ，在计算 a1 += ((b1+=c1)的结果)
        // a1 += (b1 += c1);   // 与上面等价
        
        int result1 = a1 + b1 - c1; // 因为+ 和 - 同级，并且与数学运算顺序一样，从左至右
        // int result1 = (a1 + b1) - c1;   // 与上面等价
        // 其他不一一举例，有需要看请看书里相关章节的表
        
    }
}

```

关于负数介绍[点击这里](https://www.csdn.net/gather_2f/NtjaEgwsMDM0LWJsb2cO0O0O.html)，剩下的看代码

> Strings.java

```java
import java.io.IOException;
import java.io.PrintWriter;
import java.nio.file.Paths;
import java.util.*;

public class Strings {
    public static void main(String[] args) throws IOException
    {
        // 字符串，就是由字符组成的串（貌似废话-。-）
        String e = "";  // 定义了一个空字符串，定义方式与其他变量一样，不在赘述。这里注意S一定要大写
        String greeting = "HelloWorld";

        // 字串操作
        String s = greeting.substring(0, 3); // 从greeting中提取字符串，然后赋给新的变量，两个参数分别表示，从哪个位置开始（从0开始，大部分编程语言的默认索引都是从0开始）、到哪个位置结束（不包含当前数字位置）
        System.out.println(s); // 输出：Hel

        // 拼接
        String expletive = "Expletive";
        String PG13 = "deleted";
        String message = expletive + PG13; // 直接使用加号，将两个字符串拼接起来，赋值给message
        System.out.println("message = " + message); // 输出：message = Expletivedeleted

        int age = 13;
        String rating = "PG" + age; // 可以用其他类型与字符串进行拼接，int将转换成String，任何一个对象都可以转换成字符串，后续有详细讲解
        System.out.println("rating = " + rating); // 输出：rating = PG13

        String all = String.join(" /" , "S", "M", "L", "XL"); // 如果拼接的太多，可以考虑用String.join方法，第一个参数是拼接符，将后面N个参数（字符串）拼接起来，变成一个字符串
        System.out.println("all = " + all);  // 输出：all = S /M /L /XL

        // 这里有个概念，叫不可变字符串，即字符串是不可修改的
        greeting = "test"; // 这里的含义是，将greeting变量重新赋值成test，即在内存中重新创建一个test的字符串，然后将greeting指向test，原来的HelloWorld还在原来的内存位置，并没有被修改
        // 由于指向 HelloWorld 的变量名没有了，所以并不能再使用，不过不用担心，java 的 GC 会对这种内存进行回收，不用担心占用太多内存


        // 比较两个字符串是否相同
        System.out.println("test".equals(greeting)); // 前面可以是变量，也可以是现写的字符串，同理，参数也可以是字符串，也可以是变量
        System.out.println(greeting.equalsIgnoreCase("TEST")); // 忽略大小写的比较
        System.out.println(greeting == "test"); // ！！！不要使用 == 来比较两个字符串是否相等，因为这不可靠，由于Java的机制， == 比较的是两个字符串是否是同一个，而不是他们是否相等，由于Java会共享相同常量，所以这两个test实际是再同一个内存位置

        // 空串 和 null
        if (e.length() == 0)  // 使用字符串的长度来判断
        {
            System.out.println("e is empty String");
        }

        if (e.equals(""))    // 也可以用方法来判断
        {
            System.out.println("e allways is empty String");
        }

        String str = null;
        if (str == null)         // 用== 来判断是否是null，null与""不一样，注意需要使用的时候两个都需要判断
        {
            System.out.println("str is null");
        }


        // 码点与代码单元
        int n = greeting.length(); // 通过length()获得代码单元数量
        System.out.println(n); // 输出：4
        int cpCount = greeting.codePointCount(0, greeting.length()); // 通过.codePointCount()获取码点数量，第一个参数是从哪个位置开始
        System.out.println(cpCount); // 输出：4                      由于这里都是字母，所以与代码单元数量相同

        char first = greeting.charAt(0); // 通过.charAt()获取第N个位置的代码单元

        // 通过以下代码获取第i个码点
        int i = 2;
        int index = greeting.offsetByCodePoints(0, i);
        int cp = greeting.codePointAt(index);

        // 关于码点操作和其他StringAPI就不多演示，很多API还是很有用处的，建议多看看，最起码熟悉可以使用API做到什么操作，这样以后需要用到的时候进行查手册

        // StringBuilder 这个用的比较多，这是String可修改的版本
        StringBuilder builder = new StringBuilder();   // 这里使用了new操作符，再后续会详细讲，这里知道必须这样用就好
        builder.append("abc"); // 上面创建完StringBuilder对象之后，使用builder调用方法向对象里添加字符
        builder.append("def");
        System.out.println(builder); // 输出：abcdef
        String completedString = builder.toString(); // 也可以调用.toString()方法转成String


        // 输入输出，到现在运行程序都是直接输出，然后程序就停止了，现在可以从控制台里读取用户的输入
        Scanner in = new Scanner(System.in); // 注意这个不是Java标准库的里，所以需要导入，请注意文件顶部多的代码，这一行是new 对象
        System.out.print("what is your name? "); // 给与提示
        String name = in.nextLine();     // 从控制台等待用户输入，换行结束等待，然后将用户输入的字符串保存到name里
        System.out.println("Hello " + name);
        String firstName = in.next();    // 也是从控制台等待输入，区别就是上面的可以保存一整行，这个方法只能保存住空格之前或者换行之前的
        System.out.println(firstName); //  比如如果输入 sing ll aa bb ，那么firstName 里只会存下sing

        System.out.print("How old are you");
        int age1 = in.nextInt(); // 只读取int，读取浮点数用in.nextDouble()
        System.out.println("your age is " + age1);



        // 格式化输出
        double x = 1000.0/3.0;
        System.out.println(x);

        System.out.printf("%8.2f", x); // 使用printf方法进行格式化输出，表示小数点前方有8个字符宽度，小数点后2个字符，输出：  333.33
        System.out.println(); // 增加一个空格以分开上下两个输出的显示
        System.out.printf("%,.2f", 10000.0/3.0); // 注意使用,号分隔，便于看数字位数 输出：3,333.33

        // 格式化输出异常强大，可以有N多组合格式，没有办法都列出来，所以请看书和文档来进行组合输出


        // 文件输入和输出
        Scanner in1 = new Scanner(Paths.get("myfile.txt"), "UTF-8"); // 注意：这里需要再main附近添加抛异常的关键词，还需要导入包，请见文件头部
        // 将读取文件，将内容放到in中
        PrintWriter out = new PrintWriter("myfileout.txt","UTF-8"); // 注意：这也需要引入类库
        out.print("test out"); // 向文件中写入内容

        // 注：这里没有写路径，就是再当前路径下找文件，除了这种相对路径的方式，也可以使用绝对路径，比如C:\\mydirectory\\myfile.txt
        // 注意这里的\ 使用了两个，/ 则不用



    }
}
```

由于API众多，这里只讲怎么用，就不繁琐的每个都列以下怎么用，用到的时候查询官方手册，总是一个好办法

> ControlProcess.java

```java
public class ControlProcess {
    public static void main(String[] args)
    {
       
        // 块作用域
        int n = 1;
        {
            int i = n + 2; // 在子块中可以使用父块的变量
            // int n = 2; // 不可以在子块中定义同名变量，会冲突
        }
        // 但是在子块结束后，这里不可以使用子块里定义的变量
        // int a = i + 1; // 这是不合法的，会报错，提示没有定义i


        // 条件语句
        if(n == 1)
        {
            System.out.println("n == 1 ,会看到我"); // 根据if后面的判断条件，如果为真则执行这个代码块里的代码
        }
        // 如果为假，则跳过上面代码块，继续执行下面的语句

        if (n != 1)
        {
            System.out.println("跳过这条语句");
        }else {
            System.out.println("这个代码块会被执行"); // 可以使用if else 来执行，else表示除了上面为真的情况，执行这个代码块
        }

        if (n == 4)
        {
            System.out.println("n 是4");
        } else if (n == 2) {
            System.out.println("n 是2");
        } else if (n == 1) {
            System.out.println("猜对了");
        }else if(n == 1){
            System.out.println("但是不会再看到我了");
        } else {
            System.out.println("上面都没捕获的就交给我处理");
        }
        // 可以通过else if语句来依次来判断里面的语句是否为真，判断为真则执行代码块里的代码，然后忽略之后所有的else if 和else

        // 循环
        int i = 0;
        while(n == 1) // 当（）中的为真则执行下面的代码块，再执行一遍之后，再回到这个（），继续判断，为真则继续执行，如此循环，如果（）首次为false，则直接跳过代码块，连一次都不会执行
        {
            System.out.println(n);
            // 下面的是为了跳出循环，不然程序会一直执行，直到手动停止
            i++;
            if (i > 10){
                break; // 用来终止循环，当1 大于10 的时候，终止，终止循环之后继续沿着代码块之后的代码执行
            }
        }

        do {
            System.out.println("不论判断的结果是什么，我都会先输出一次，之后就和上面的while没区别了");
        }while(n==2);


        for (int a = 0; a >10; a ++)   // 这是一个带条件的while，自带三段式，第一个是初始化一个变量，第二个是终止条件（当a>10的时候终止循环）,第三个是每次先执行的一段代码，一般用来对变量进行增量，比如i++,或者减量i--，当然也可以加任意数，比如i+3
        {
            System.out.println(a);
            // 代码块里可以放任意代码，这点再前面的代码块也一样，比如这里可以嵌套if else， 也可以嵌套while和for

        }

        // 多重选择
        switch(n) // n来和每个case后面的进行比较，如果相同则执行下面的代码
        {
            case 1: // case标签可以是char、byte、short、int、枚举常量、字符串字面量
                System.out.println("n 是 1 ，执行这里");
                break; // 这里的break是不必须的，但是如果不加，会从这里继续执行，而不是跳出这个switch
            case 2:
                System.out.println("如果不是上面的break，你就能看到我了");
                break;
            case 3:
                System.out.println("我要在上面两个break都没有的情况下才能看到");
                break;
            default:
                System.out.println("如果上面都匹配不上，执行我就对了");
                break; // 这个加与不加没区别，为了格式整齐就加上吧
        }

        // 中断控制流程语句
        // break 在上面已经简单介绍了，其实就是忽略下面的语句，从循环开始的地方继续执行，这里注意，如果是多层嵌套循环，则从本层的循环头开始执行
        // 如果想跳的更远，可以增加标签，直接跳到标签上
        /* 这块代码在我这里不显示，后续看是什么情况
        zero:  // 标签用: 冒号来结尾
        for (int a1 = 0; a1 > 20 ; a1++)
        {

            System.out.println(a1);
            for (int a2 = 0; a2 >20; a2 ++)
            {
                if(a2 == 10){
                    break zero; // 到10 就不输出了
                }
                System.out.println(a2);

            }
        }
        
         */

        // continue与break一样，也是跳过剩下的代码
        


    }
}
```

分为if，if else ，if else if else，while，for，switch，这些控制流程，都是很简单的结构，看看代码就知道了

> BigNumber.java

```java
import java.math.BigInteger;

public class BigNumber {
    public static void main(String[] args)
    {
        // 大数值
        BigInteger a = BigInteger.valueOf(100); // 可以通过valueOf() 来进行转换
        BigInteger b = BigInteger.valueOf(200);
        BigInteger c = a.add(b); // 运算的话必须通过这种调用方法的形式，而不可以用四则运算符，并且参数必须是大数值格式，不能是int等，这是进行a+b
        BigInteger d = c.multiply(b.add(BigInteger.valueOf(2))); // d = c * (b+2)

        // 解锁更多方法请看手册和书，不是需要很精准的地方一般用不到
    }
}
```

略

> Arrayst.java

```java
import java.util.*;

public class Arrayst {
    public static void main(String[] args)
    {
        // 数组

        int[] a; // 声明int型数组 a，这里也可以写成 int a[]; 数组里必须存放int型
        a = new int[100]; // 初始化数组，必须在用之前就确定数组是多少个元素，在后面int[]里存放的数组一共有多少个元素

        int[] b = new int[200]; // 也可以直接初始化
        // 初始化的时候，int数组在没赋值的情况下，每个元素都是0，boolean数组是false，对象数组是null

        a[10]  = 100;   // 可以通过下标来对单个进行赋值
        System.out.println(a[10]); //可以直接按下标来取，注意下标是从0开始，即a[0]是第一个元素，以此类推，a[100-1]即是最后一个元素，a[n-1] n为数组元素个数
        for (int i = 0; i < 100; i ++)   // 常见的用法是用循环进行赋值
        {
            a[i] = i;
        }

        for (int i = 0; i < 100 ; i ++)
        {
            System.out.println(a[i]);// 通过循环来遍历输出数组各个元素
        }

        for(int a3 : a) // foreach 是系统自带的简单的for实现，语法是for(变量：数组)   这样就不用自己设置循环次数，foreach会保证每个元素循环到
        {
            System.out.println(a3);
        }

        // 数组拷贝
        int[] lockyNumbers = a;
        a[0] = 123;
        System.out.println(lockyNumbers[0]);// 注意，这里两个数组使用的是同一组数据，改一个另一个也会变,输出：123

        lockyNumbers = Arrays.copyOf(a, a.length); // 如果希望各自维护一套元素，则使用copyOf来进行拷贝
        a[1] = 234;
        System.out.println(lockyNumbers[1]);// 输出：1

        // main方法的参数args就是一个数组，从命令行进行读取参数，放到args里
        // 如果运行 java Arrayst.java test aaa bbb
        // 则args[0] = "test"，args[1] = "aaa" ，args[2] = "bbb"

        // 数组排序
        Arrays.sort(a); // 对数组进行了排序

        // 多维数组
        int[][] magicSquare =
                {
                        {16, 3, 2, 13},
                        {5, 10, 11, 8},
                        {9, 6, 7, 12},
                        {4, 15, 14, 1}
                };
        // 多维数组的初始化，一维数组也可以直接初始化，注意用{}来进行初始化

        for (int i = 0; i < magicSquare.length;i++)  // 多维数组的遍历方式，即循环嵌套循环
        {
            for (int j =0; j < magicSquare[i].length; j++)
            {
                System.out.println(magicSquare[i][j]);
            }
        }

        // 二维数组的第二维不是必须长度相同，可以每个都不同，利用循环初始化


    }
}
```

String[] str 就是字符串数组，里面没有写，但是应该清楚