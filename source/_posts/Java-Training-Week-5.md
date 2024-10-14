---
title: '[Java Training]Week 5'
date: 2019-12-15 20:32:14
categories: Java
tags: Java
index_img: https://i.loli.net/2019/07/07/5d21cd23675da29020.jpg
---

# 0x00

​    本系列-Java集训系列

​    记录我带领小组进行Java学习，按照《Java核心技术》第十版进行学习

# 0x01

​    接口、lambda、内部类

# 0x02

1. 接口(Interface)是对类的一组需求描述,这些类要遵从接口描述的统一格式进行定义

2. 可以将接口看成没有属性的抽象类（看成的意思就是两者有一些区别，但是大体上是差不多的）

3. 定义接口：***public interface interfacename{}*** 

4. 实现接口：***public class classname implements interfacename1,interfacename2{}***

5. 可以看到接口与抽象类很像，不过有个最大的不同就是一个类可以实现任意个接口，而一个类只能继承一个抽象类，这样就导致了使用方法上有很大不同

6. 在接口中定义的方法，实现接口的类必须实现，除非加**default**描述符，在定义方法的时候将此关键字加到前面，并且在接口中实现一个默认方法，就可以在实现接口的类中不实现此方法，使用默认的方法（有点绕，看代码）

7. 如果先在一个接口中将一个方法定义为默认方法，然后又在超类或另一个接口中定义了同样的方法，就会产生冲突，以下是Java在解决冲突方面的规则

   1）超类优先。如果超类提供了一个具体方法，同名而且具有相同参数类型的默认方法会被忽略。

   2）接口冲突。如果一个超接口提供了一个默认方法，另一个接口提供了一个同名而且参数类型相同的方法，必须覆盖这个方法来解决冲突
   
8. 如果一个类实现的两个接口中定义了同样的方法，并且至少其中一个是**默认(default)**方法，则实现类必须要覆盖方法，选择手动选择其中一个来调用

> 接口的定义和实现

> InterfaceTest.java

```java
package cc.singll.learnjava.interfaces;

// 这里是对接口进行测试的主类
public class InterfaceTest{
    public static void main(String[] args)
    {
        // 使用的时候可以用接口的类型来定义变量，但是实例化的是实现接口的类，而不能实例化接口，并且这里不可以用 C_INT
        Customizee<Person> persona = new Person("Tony", 22, 1);
        
        // 当然也可以用Person来定义变量
        Person personb = new Person("Tom", 25, 0);
        
        // 就可以在这里调用实现的接口了
        boolean agtb = persona.greaterThan(personb);

        System.out.println("a gt b ?" + agtb);

        int reta = persona.ret();
        int retb = personb.ret();

        System.out.println("reta = " + reta + ", retb = " + retb);


    }
}

```

> Person.java

```java
package cc.singll.learnjava.interfaces;

// 实现了自定义接口的类，关键字 implements interfacename 代表实现接口
public class Person implements Customizee<Person> {
    private String name;
    private int age;
    private int sex;

    public Person(String name, int age, int sex)
    {
        this.name = name;
        this.age = age > 0 ? age:0;
        this.sex = sex == 0 ? 0:1;
    }

    public String getName()
    {
        return name;
    }

    public int getAge()
    {
        return age;
    }

    public String getSex()
    {
        return age==0?"男":"女";
    }

    // 这是接口 Customize 的方法，由于没有使用default，所以必须实现（由于继承）
    public boolean greaterThan(Person a)
    {
        // 这里可以使用静态属性，不过不是很建议使用，知道可以这么用就好了
        return this.age+C_INT>a.age+C_INT?true:false;
    }
}

```

> Customizee.java

```java
package cc.singll.learnjava.interfaces;

// 可以用 extends 扩展接口，就像继承一样（这里是使用继承来扩展接口，本身也是个接口。）
public interface Customizee<T> extends Customize<T> {

    // 默认方法，实现接口的类可以选择覆盖或者不覆盖，不覆盖就是用的接口里的实现方式，比如这里就是返回0
    default int ret(){return 0;}
}

```

> Customize.java

```java
package cc.singll.learnjava.interfaces;

// 接口定义用关键词 interface 代替 class
public interface Customize<T> {

    // 虽然接口不能包含属性，但是可以包含常量
    // 这里其实是 public static final double C_INT = 20
    double C_INT = 20;


    // 接口定义的方法，必须实现的
    boolean greaterThan(T a);

    /*
    // 这个方法会报错，不可以更改final值
    default double setC_INT(int a)
    {
      this.C_INT = a;
    };
     */
}

```

> 书中实现基础接口和调用的示例（就不细标示出了）

> EmployeeSortTest.java

```java
package cc.singll.learnjava.interfaces;

import java.util.*;

public class EmployeeSortTest {
    public static void main(String[] args)
    {
        Employee[] staff = new Employee[3];

        staff[0] = new Employee("Harry Hacker", 35000);
        staff[1] = new Employee("Carl Cracker", 75000);
        staff[2] = new Employee("Tony Tester", 38000);

        Arrays.sort(staff);

        // print out information about all Employee objects
        for (Employee e : staff)
            System.out.println("name=" + e.getName() + ",salary=" + e.getSalary());
    }
}

```

> Employee.java

```java
package cc.singll.learnjava.interfaces;

public class Employee implements Comparable<Employee> {
    private String name;
    private double salary;

    public Employee(String name, double salary)
    {
        this.name = name;
        this.salary = salary;
    }

    public String getName()
    {
        return name;
    }

    public double getSalary()
    {
        return salary;
    }

    public void raiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }

    /**
     * Compares employees by salary
     * @param other another Employee object
     * @return a negative value if this employee has a lower salary than
     * otherObject, 0 if the salaries are the same, a positive value otherwise
     */

    public int compareTo(Employee other)
    {
        return Double.compare(salary, other.salary);
    }
}

```



回调是一种常见的程序设计模式，指出某个特定事件发生时应该采用的动作。

简单理解就是延迟调用，普通的代码都是顺序的，执行到就执行了，回调就是先将定义好的代码放到某个位置，然后等到满足条件的时候就调用那部分代码。

> TimerTest.java

```java
package cc.singll.learnjava.timer;

import java.awt.*;
import java.awt.event.*;
import java.util.*;
import javax.swing.*;
import javax.swing.Timer;

public class TimerTest {
    public static void main(String[] args)
    {
        ActionListener listener = new TimePrinter();

        // construct a timer that calls the listener
        // once every 10 seconds
        // 每十秒调用一次 listener.actionPerformed，传进去的是一个对象
        Timer t = new Timer(10000, listener);
        // 调用start()才是正式开始运行
        t.start();
        // 显示一个对话框，这里主要是为了阻塞进程和方便推出，阻塞进程的意思是由这句占用主进程，打印日期和响声的代码并不是这里调用，而是回调调用的
        JOptionPane.showMessageDialog(null, "Quit program?");
        System.exit(0);
    }
}

class TimePrinter implements ActionListener
{
    // 实现接口，接口 ActionListener 只有这一个方法
    public void actionPerformed(ActionEvent event)
    {
        System.out.println("At the tone, the time is " + new Date());
        // 这句代码是响一声
        Toolkit.getDefaultToolkit().beep();
    }
}

```

克隆，clone是Object的一个protected方法，所以自定义的类想要克隆就要覆盖clone方法并将修饰符变成public

Object的clone方法默认是"浅拷贝"，即如果属性是可变的（比如各种对象类型），则只拷贝引用，不拷贝一份完整的对象

想要进行"深拷贝"就要自己实现

> CloneTest.java

```java
package cc.singll.learnjava.clone;

public class CloneTest {
    public static void main(String[] args)
    {
        try
        {
            // 先定义一个original
            Employee original = new Employee("John Q. Public", 50000);
            original.setHireDay(2000, 1, 1);
            // 调用clone()方法，克隆一份
            Employee copy = original.clone();
            
            // 调用方法更改属性
            copy.raiseSalary(10);
            copy.setHireDay(2002, 12, 31);
            
            // 输出两个对象，发现内容不同
            System.out.println("original=" + original);
            System.out.println("copy=" + copy);
        }
        catch (CloneNotSupportedException e)
        {
            e.printStackTrace();
        }
    }
}

```

> Employee.java

```java
package cc.singll.learnjava.clone;

import java.util.Date;
import java.util.GregorianCalendar;

// 实现Cloneable方法，这个方法不是必须的，只是约定实现此接口的类肯定可以Clone
public class Employee implements Cloneable {
    private String name;
    private double salary;
    private Date hireDay;

    public Employee(String name, double salary)
    {
        this.name = name;
        this.salary = salary;
        hireDay = new Date();
    }

    // 克隆方法，首先调用Object的clone方法，然后将可变的对象（Date）clone一下
    public Employee clone() throws CloneNotSupportedException
    {
        // call Object.clone()
        Employee cloned = (Employee) super.clone();

        // clone mutable fields
        cloned.hireDay = (Date) hireDay.clone();

        return cloned;
    }

    /**
     * Set the hire day to a given date.
     * @param year the year of the hire day
     * @param month the month of the hire day
     * @param day the day of the hire day
     */
    public void setHireDay(int year, int month, int day)
    {
        Date newHireDay = new GregorianCalendar(year, month - 1, day).getTime();
        // Example of instance field mutation
        hireDay.setTime(newHireDay.getTime());
    }

    public void raiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }

    public String toString()
    {
        return "Employee[name=" + name + ",salary=" + salary + ",hireDay=" + hireDay + "]";
    }
}

```

lambda表达式是一个可传递的代码块。

首先是什么地方需要使用lambda表达式，在需要回调的地方，并且回调需要的代码只执行一两次，就可以用lambda，而不是用上例那样再定义一个类，很繁琐。

然后，lambda表达式语法：

1. 完整形式：(type name1,type name2)->{ xxxxx;return xx;}
2. 首先是一个括号，括号里是标准的参数类型+参数名称，然后一个->，最后一个代码块，代码块里要有返回值
3. 省略形式：(name1,name2)->{xxxx;return xx;}//如果参数类型可以推导出来，那么就可以省略
4. 省略形式：()->{xxx;return xx;}//如果没有参数就空的括号
5. 省略形式：name->{xxx;return xx;}//如果只有一个参数，可以省略括号和类型
6. 省略形式：()->xxx; //如果代码只有一行，并且是返回值，可以不用return，代码执行结果就当作返回值
7. 如果代码块里由分支，那么其中一个有返回值，另一个必须有返回值

> LambdaTest.java

```java
package cc.singll.learnjava.lambda;

import java.util.*;
import javax.swing.*;
import javax.swing.Timer;

public class LambdaTest {
    public static void main(String[] args)
    {
        String[] planets = new String[] {"Mercury", "Venus", "Earth", "Mars", "Jupiter", "Saturn", "Uranus", "Neptune"};
        System.out.println(Arrays.toString(planets));
        System.out.println("Sorted in dictionary order:");
        Arrays.sort(planets);
        System.out.println(Arrays.toString(planets));
        System.out.println("Sorted by length:");
        // 省略了参数类型和return的lambda表达式
        Arrays.sort(planets, (first, second)->first.length()-second.length());
        System.out.println(Arrays.toString(planets));

        // 省略了类型和括号，还省略了return的lambda表达式
        Timer t = new Timer(1000, event->System.out.println("The time is " + new Date()));
        t.start();

        // keep program running until user selects "OK"
        JOptionPane.showMessageDialog(null, "Quitprogram?");
        System.exit(0);
    }
}

```

方法引用是一个语法糖，即编译器进行优化的语法。

方法引用等价于lambda表达式，比如System.out::println 等价于 x->System.out.println(x)

方法引用有如下三种形式

1. *object*::*instanceMethod*
2. *Class*::*staticMethod*
3. *Class*::*instanceMethod*

前两种情况，方法引用等价于提供方法参数的lambda表达式。

第一种：System.out.println 等价于 x->System.out.println(x)

第二种：Math::pow 等价于 （x,y）->Math.pow(x,y)

第三种：String::compareToIgnoreCase 等价于 (x,y)->x.compareToIgnoreCase(y)

this::equals 等价于 x->this.equals(x)

*super*::*instanceMethod* 也一样

构造器引用：*Class*::*new*

关于变量作用域，看书就好了，多看看才能理解

主要问题在于，如果引用外部变量，是有一定规则的。



lambda表达式使用，lambda表达式的特点是延迟执行，而不是立刻运行，因为一般的代码都是立刻运行的，也不需要用lambda，那么用lambda表的是的需求原因典型有如下：

1. 在一个单独的线程中运行代码；
2. 多次运行代码；
3. 在算法的适当位置运行代码（例如，排序中的比较操作）；
4. 发生某种情况时执行代码（如，点击了一个按钮，数据到达，等等）；
5. 只有在必要时才运行的代码。

可能会有疑问为什么延迟执行就要用lambda，而不是写个类来调用？

答案是lambda想执行的代码是临时定义的，或者说是多样的、动态的，与直接定义在类里的有本质区别

比如以下一个场景，重复执行一个片段代码N次：

> repeat(10, () -> System.out.println("Hello, World!"));

可以在调用这个方法的时候，传进去任意代码片段的lambda表达式，这样可以很方便的达到目的，也很灵活

上面的repeat定义如下，并不是随便可以接收lambda参数：

```java
public static void repeat(int n, Runnable action)
{
    for (int i = 0; i < n; i++) action.run();
}
```

> 常用函数式接口

| 函数式接口        | 参数类型 | 返回类型 | 抽象方法名 | 描述                         | 其他方法                 |
| ----------------- | -------- | -------- | ---------- | ---------------------------- | ------------------------ |
| Runnable          | 无       | void     | run        | 作为无参数或返回值的动作执行 |                          |
| Supplier<T>       | 无       | T        | get        | 提供一个T类型的值            |                          |
| Consumer<T>       | T        | void     | accept     | 处理一个T类型的值            | addThen                  |
| BiConsumer<T,U>   | T,U      | void     | accept     | 处理T和U类型的值             | addThen                  |
| Function<T,R>     | T        | R        | apply      | 有一个T类型参数的函数        | compose,andThen,identity |
| BiFunction<T,U,R> | T,U      | R        | apply      | 有T和U类型参数的函数         | addThen                  |
| UnaryOperator<T>  | T        | T        | apply      | 类型T上的一元操作符          | compose,andThen,identity |
| BinaryOperator<T> | T,T      | T        | apply      | 类型T上的二元操作符          | addThen,maxBy,minBy      |
| Predicate<T>      | T        | boolean  | test       | 布尔值函数                   | and,or,negate,isEqual    |
| BiPredicate<T,U>  | T,U      | boolean  | test       | 有两个参数的布尔值函数       | and,or,negate            |

> 基本类型的函数式接口

| 函数式接口         | 参数类型 | 返回类型 | 抽象方法名   |
| ------------------ | -------- | -------- | ------------ |
| BooleanSupplier    | none     | boolean  | getAsBoolean |
| PSupplier          | none     | p        | getAsP       |
| PConsumer          | p        | void     | accept       |
| ObjPConsumer<T>    | T,p      | void     | accept       |
| PFunction<T>       | p        | T        | apply        |
| PToQFunction       | p        | q        | applyAsQ     |
| ToPFunction<T>     | T        | p        | applyAsP     |
| ToPBiFunction<T,U> | T,U      | p        | applyAsP     |
| PUnaryOperator     | p        | p        | applyAsP     |
| PBinaryOperator    | p,p      | p        | applyAsP     |
| PPredicate         | p        | boolean  | test         |

也可以自定义接口，不过推荐使用内置的



内部类基本等同于类，只不过是在类的内部，特点是可以使用所在的类的属性，语法很简单易懂，仔细理解还是比较麻烦的，可以多看看这一章关于内部类的解释

> InnerClassTest.java

```java
package cc.singll.learnjava.innerClass;

import java.awt.*;
import java.awt.event.*;
import java.util.*;
import javax.swing.*;
import javax.swing.Timer;

public class InnerClassTest {
    public static void main(String[] args)
    {
        TalkingClock clock = new TalkingClock(1000, true);
        clock.start();

        // keep program running until user selects "OK"
        JOptionPane.showMessageDialog(null, "Quit program?");
        System.exit(0);
    }
}

/**
 * A clock that prints the time in regular intervals
 */
class TalkingClock
{
    private int interval;
    private boolean beep;

    public TalkingClock(int interval, boolean beep)
    {
        this.interval = interval;
        this.beep = beep;
    }

    /**
     * Starts the clock.
     */
    public void start()
    {
        ActionListener listener = new TimePrinter();
        Timer t = new Timer(interval, listener);
        t.start();
    }

    // 内部类 TimePrinter
    public class TimePrinter implements ActionListener
    {
        public void actionPerformed(ActionEvent event)
        {
            System.out.println("At the tone, the time is " + new Date());
            // 这里的 beep 引用的是外围的 beep
            if (beep) Toolkit.getDefaultToolkit().beep();
        }
    }
}

```

局部内部类，就是在方法内的内部类，只有方法内可以使用，其他方法不可以使用，也是可以访问所在类的属性

优点就是可以访问方法内部的局部变量

匿名内部类，如果内部类只使用了一次，即只有一次实例化，那么可以使用匿名内部类，语法为：

new SuperType(construction prarmeters)

{

​	innter class methods and data

}

中文版 :

new 父类或者接口名(父类构造器参数)

{

​	内部类的方法或者属性

}

可以对比一下正常的实例化与匿名内部类的实例化

```java
// 正常实例化
Person queen = new Person("Mary");
// 匿名内部类
Person count = new Person("Dracula") {
    public void printname(){
        System.out.println(this.name);
    }
}
```

> AnonymousInnerClassTest.java

```java
package cc.singll.learnjava.anonymousInnerClass;

import java.awt.*;
import java.awt.event.*;
import java.util.*;
import javax.swing.*;
import javax.swing.Timer;

public class AnonymousInnerClassTest {
    public static void main(String[] args)
    {
        TalkingClock clock = new TalkingClock();
        clock.start(1000, true);

        // keep program running until user selects "OK"
        JOptionPane.showMessageDialog(null, "Quit program?");
        System.exit(0);
    }
}

/**
 * A clock that prints the time in regular intervals.
 */
class TalkingClock
{
    public void start(int interval, boolean beep)
    {
    	// 匿名内部类
    	// 这里是实现了ActionListener 接口
        ActionListener listener = new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent event) {
                System.out.println("At the tone, the time is " + new Date());
                if (beep) Toolkit.getDefaultToolkit().beep();
            }
        };
        Timer t = new Timer(interval, listener);
        t.start();
    }
}

```

如果内部类没有引用任何外部的变量，那么可以定义为静态内部类，然后被外部使用

> StaticInnerClassTest.java

```java
package cc.singll.learnjava.staticInnerClass;

public class StaticInnerClassTest {
    public static void main(String[] args)
    {
        double[] d = new double[20];
        for (int i = 0; i < d.length; i++)
            d[i] = 100 * Math.random();
        ArrayAlg.Pair p = ArrayAlg.minmax(d);
        System.out.println("min = " + p.getFirst());
        System.out.println("max = " + p.getSecond());
    }
}

class ArrayAlg
{
    /**
     * A pair of floating-point numbers
     */
    public static class Pair
    {
        private double first;
        private double second;

        public Pair(double f, double s)
        {
            first = f;
            second = s;
        }

        public double getFirst()
        {
            return first;
        }

        public double getSecond()
        {
            return second;
        }
    }
    // 静态内部类，用static修饰
    public static Pair minmax(double[] values)
    {
        double min = Double.POSITIVE_INFINITY;
        double max = Double.NEGATIVE_INFINITY;
        for (double v : values)
        {
            if (min > v) min = v;
            if (max < v) max = v;
        }
        return new Pair(min, max);
    }
}

```



本章最后一部分，代理

这是一个设计模式，即通过一个代理类来进行调用，不是直接调用，就像平常的代理概念一样，比如如果想看404的网站，那么就可以使用代理。

代理可以实现一些目标：

1. 路由对远程服务器的方法调用
2. 在程序运行期间，将用户接口事件与动作关联起来
3. 为调试，跟踪方法调用

比较难理解，这部分就看一看示例，多看看书，不理解就以后再看

> ProxyTest.java

```java
package cc.singll.learnjava.proxy;

import java.lang.reflect.*;
import java.util.*;

public class ProxyTest {
    public static void main(String[] args)
    {
        Object[] elements = new Object[1000];

        // fill elements with proxies for the integers 1 ... 100
        for (int i = 0; i < elements.length; i++)
        {
            Integer value = i + 1;
            // 初始话代理类
            InvocationHandler handler = new TraceHandler(value);
            // 这里是真正的代理 将hook的方法与代理对象绑定，比如这里是Compareable的class，然后代理类就是TreaceHandler
            Object proxy = Proxy.newProxyInstance(null, new Class[] {Comparable.class}, handler);
            // 这里赋值时为了从代理调用，而不是直接调用，可以说最基本的改变就是这里
            elements[i] = proxy;
        }

        // construct a random integer
        Integer key = new Random().nextInt(elements.length) + 1;

        // search for the key
        int result = Arrays.binarySearch(elements, key);

        // print match if found
        if (result >= 0) System.out.println(elements[result]);
    }
}

// 用于跟踪方法调用的代理对象
class TraceHandler implements InvocationHandler
{
    private Object target;

    // 初始化 target
    public TraceHandler(Object t)
    {
        target = t;
    }

    public Object invoke(Object proxy, Method m, Object[] args) throws Throwable
    {
    	// 这里是跟踪打印的部分
    	// 其实就是在直接调用中间插入一个步骤，然后你就可以在调用之前进行一些操作，类似劫持、钓鱼
        // print implicit argument
        System.out.print(target);
        // print method name
        System.out.print("." + m.getName() + "(");
        // print explicit arguments
        if (args != null)
        {
            for (int i = 0; i < args.length; i++)
            {
                System.out.print(args[i]);
                if (i < args.length - 1) System.out.print(",");
            }
        }

        System.out.println(")");

        // 这里是真正调用的部分
        // invoke actual method
        return m.invoke(target, args);
    }
}

```

# 0x03

相当懒的我终于回来更新了，也终于继续学Java了

本文前半段的更新时间是 2019-09-03 20:32:14

后半段就如文章首部的时间

真的是相当无语，不过继续学就是了

插播一条，明年的新年目标要立在blog上

打脸见~~