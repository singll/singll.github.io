---
title: '[Java Training]Week 3'
date: 2019-08-03 15:33:19
categories: Java
tags: Java
index_img: https://i.loli.net/2019/07/07/5d21cd23675da29020.jpg
---
# 0x00
    本系列-Java集训系列
    记录我带领小组进行Java学习，按照《Java核心技术》第十版进行学习
# 0x01
    开始面向对象
# 0x02
首先声明，对象怎么理解什么的就不再赘述了，这个书里讲的很详细，我这里主要记录一下基本定义和语法怎么写
1. 类：所有Java代码都属于某个类，有标准的Java库里的类，也有第三方库里的类，还有自定义的类
2. 封装：通过控制类里各个元素的访问权限，来达到封装的目的
3. 对象：类的实例，对象与类的关系类似于变量与类型，可以通过对象来调用类里定义的方法和访问类里的属性（这里说类不是很贴切，确切的说是此对象的属性和方法，因为实例化对象之后，正常对于此对象的操作不会影响到类里，也不会影响到其他对象，不过方法和属性是在类里定义的，也是在类里实现的）
4. 类与类之间有三种关系：
    * 依赖：A类里的方法使用了B类里的方法，就说A依赖B，而B不依赖A
    * 聚合：A类包含B类，就是聚合
    * 继承：B类在A类的基础上进行扩展或重写，就是继承
以下为调用Java标准类库的一个示例代码

> CalendarTest.java

```java
package CalendarTest;

//导入类库，虽然是Java标准类库，但是除了几个基本的，其他都需要导入，不然无法使用
import java.time.*;

//定义类   public 是公开的，谁都可以使用这个类  class 关键词，定义类的时候必须要写的   CalendarTest 是类名，一个Java文件里必须有一个与文件名一致的类，并且一定要用public修饰，如果同一个文件里有多个类，那么其他的类都不可以带任何修饰符，形如 class test{}    类名后面跟着的是由一对大括号组成的块，块里所有的代码都属于这个类
public class CalendarTest {

    // public 是与类修饰符一样的意义 static是静态方法的修饰符，这里定义是因为main方法必须由static修饰  void 这里是返回值类型，由于main方法没有返回值，所以由void代替，如果是其他方法，有返回值，此处是返回值的类型，可以是基础类型，也可以是对象类型   main 就是方法名，这里的main是固定的，其他方法可以自由命名，命名规则同变量   括号里的就是参数，多个参数用逗号（,）分隔，参数的形式就是：数据类型 变量名。
    public static void main(String[] args)
    {
        // 这里是调用的LocalDate类的new()方法，这个是静态方法的调用方式，然后赋值给一个LocalDate对象
        LocalDate date = LocalDate.now();
        
        // 使用date（LocalDate对象）来进行调用方法
        int month = date.getMonthValue();
        int today = date.getDayOfMonth();

        // 以下可以自己运行一下，看一看输出
        date = date.minusDays(today - 1); // Set to start of month
        DayOfWeek weekday = date.getDayOfWeek();
        int value = weekday.getValue();  // 1 = Monday, ... 7 - Sunday

        System.out.println("Mon Tue Wed Thu Fri Sat Sun");
        for (int i = 1; i < value; i++) {
            System.out.print("    ");
        }
        while (date.getMonthValue() == month)
        {
            System.out.printf("%3d", date.getDayOfMonth());
            if (date.getDayOfMonth() == today){
                System.out.print("*");
            } else {
                System.out.print(" ");
            }
            date = date.plusDays(1);
            if (date.getDayOfWeek().getValue() == 1) System.out.println();
        }
        if (date.getDayOfWeek().getValue() != 1) System.out.println();
    }
}
```

以下是自定义类的示例：
> EmployeeTest.java

```java
package EmployeeTest;
// 上面的是包名，Java使用包来分隔不同的类，以达到方便定位，方便命名的作用

import java.time.*;

// 定义类，注意此类与文件名一致，并且大小写相同
public class EmployeeTest {
    public static void main(String[] args)
    {
        // 创建Employee的数组，有三个元素，Employee在下面定义的
        // fill the staff array with three EmployeeTest.Employee objects
        Employee[] staff = new Employee[3];

        // j实例化对象，使用new 关键字，new classname()，括号里的是参数，实例化的时候会调用构造方法
        staff[0] = new Employee("Carl Cracker", 75000, 1987, 12, 15);
        staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
        staff[2] = new Employee("Tony Tester", 40000, 1990, 3, 15);

        // rise everyone's salary by 5%
        for (Employee e : staff)
        {
            // 使用对象调用方法
            e.raiseSalary(5);
        }

        // print out information about all EmployeeTest.Employee objects
        for (Employee e : staff)
        {
            System.out.println("name=" + e.getName() + ", salary=" + e.getSalary() + ", hireDay=" + e.getHireDay());
        }
    }
}

// 注意，这里由于是一个文件里的第二个类，所以一定不要使用修饰符，此类的可见范围是包内可见
class Employee
{
    // 定义属性 private是私有的，可见范围是类内，也就是说只有Employee类可以使用这个name  ， String是类型，同样，可以使用对象来作为类型    可以在后面直接赋初始值
    private String name = "test";
    private double salary;
    private LocalDate hireDay;

    // 构造方法 方法名与类名相同，可以有多个构造方法，但是参数不同，构造方法没有返回值，可以看到这个类里没有main方法，这是因为只需要一个入口方法。 这里定义了五个参数，并且在方法体里将获取到的参数赋值给属性
    public Employee(String n, double s, int year, int month, int day)
    {
        // 将传进来的参数值赋值给属性name
        name = n;
        salary = s;
        hireDay = LocalDate.of(year, month, day);
    }

    // 由于属性是private ，所以这里有一个public的方法来暴露给外界，以供获取name的值
    public String getName()
    {
        return name;
    }

    public double getSalary()
    {
        return salary;
    }

    public LocalDate getHireDay()
    {
        return hireDay;
    }

    // 普通方法，如果没有返回值就用void，如果有返回值就在void的位置填返回值类型
    public void raiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }
}
```

声明一下访问控制符（类内的，不包括类）：
1. public     公开，全局可访问，并且可以继承的（即任何一个类都可以访问这个属性/方法）
2. protected  继承，类内可访问，并且可以继承下去
3. private    私有，只有类内可以访问
4. 无         即修饰符位置为空，表示包内可访问
构造方法（构造器）：
1. 构造方法与类名相同
2. 每个类可以有一个以上的构造方法（但是不可以有参数个数和类型完全相同的两个构造方法）
3. 构造方法可以有任意多个参数
4. 构造方法没有返回值
5. 构造方法总是伴随着new操作一起调用
final 关键词修饰属性的时候，使属性拥有不可改变的特性

> StaticTest.java

```java
package StaticTest;

public class StaticTest {
    public static void main(String[] args)
    {
        // fill the staff array with three EmployeeTest.StaticTest.Employee objects
        Employee[] staff = new Employee[3];

        staff[0] = new Employee("Tom", 40000);
        staff[1] = new Employee("Dick", 60000);
        staff[2] = new Employee("Harry", 65000);

        // print out information about all Employee objects
        for (Employee e : staff)
        {
            e.setId();
            System.out.println("name = " + e.getName() + ", id = " + e.getId() + ", salary = " + e.getSalary());
        }

        int n = Employee.getNextId();  // calls static method
        System.out.println("Next available id=" + n);

    }
}

class Employee
{
    // 静态属性，这个属性属于类，正常的属性是每个对象都有自己的一份不同属性，当对象更改自己的属性的值的时候不会影响到其他对象，但是静态属性是所有对象共用一个，当某个对象调用方法或直接更改静态属性的时候，所有的对象访问这个属性就会发现都发生改变了
    private static int nextId = 1;

    private String name;
    private double salary;
    private int id;

    public Employee(String n , double s)
    {
        name = n;
        salary = s;
        id = 0;
    }

    public String getName()
    {
        return name;
    }

    public double getSalary()
    {
        return salary;
    }

    public int getId()
    {
        return id;
    }

    public void setId()
    {
        id = nextId;  // set id to next available id
        nextId++;
    }

    // 静态方法，也是属于类，调用方式是 类名.静态方法名（参数）   比如 Employee.getNextId()  ，而且不可以用对象调用
    public static int getNextId()
    {
        return nextId;  // returns static field
    }

    public static void main(String[] args)     // unit test
    {
        Employee e = new Employee("Harry", 50000);
        System.out.println(e.getName() + " " + e.getSalary());
    }
}

```

> ParamTest.java

```java
package ParamTest;

public class ParamTest {
    public static void main(String[] args)
    {
        /*
         * Test 1: Methods can't modify nemeric parameters
         */
        // 参数的按值传递
        // 即调用方法的时候是将值传过去的，在方法内部做的更改都不会反映到原变量
        // 用以下例子解释，调用 tripleValue的时候 是将 10 传过去了，而不是将变量percent传过去的，所以在tripleValue里的更改是在 数值 10 的基础上改，而不是改的percent变量
        System.out.println("Testing tripleValue:");
        double percent = 10;
        System.out.println("Before: percent = " + percent);
        tripleValue(percent);
        System.out.println("After: percent = " + percent);

        /*
         * Test2: Methods can change the state of object parameters
         */
        // 这里看到输出的是改完之后的值，因为传的是对象，但是还是按值传递
        // 这里传过去的是harry变量的值，在上面的例子是 数值10  ，但是这里由于是对象，不是基础类型，所以传过去的是一个“值”，这个值是对象的ID
        // 所以可以很简单的理解，由于传进去的ID没有改，而是通过ID调用对象里的方法，由于方法里的ID和变量的ID是同一个值，所以用的是同一个对象的方法，这个方法改变了属性，所以对象的状态发生改变，在外面获取属性的时候，就是改变之后的属性
        System.out.println("\nTest tripleSalary:");
        Employee harry = new Employee("Harry", 50000);
        System.out.println("Before: salary = " + harry.getSalary());
        tripleSalary(harry);
        System.out.println("After: salary = " + harry.getSalary());

        /*
         * Test 3: Methods can't attach new objects to object parameters
         */
        // 这里是为了证明传递的对象不是按引用传递
        // 由于传进去的是一个值的复制，对于值的更改，不会反应到原变量
        // 注意的点就是，虽然这里是对象，但是对象与基础类型的不一样的地方仅仅是，相同的对象的“值”可以操作同一个对象
        System.out.println("\nTesting swap:");
        Employee a = new Employee("Alice", 70000);
        Employee b = new Employee("Bob", 60000);
        System.out.println("Before: a = " + a.getName());
        System.out.println("Before: b = " + b.getName());
        swap(a, b);
        System.out.println("After: a = " + a.getName());
        System.out.println("After: b = " + b.getName());
    }

    public static void tripleValue(double x)  //doesn't work
    {
        x = 3 * x;
        System.out.println("End of method: x = " + x);
    }

    public static void tripleSalary(Employee x) // works
    {
        x.raiseSalary(200);
        System.out.println("End of method: salary = " + x.getSalary());
    }
    public static void swap(Employee x, Employee y)
    {
        Employee temp = x;
        x = y;
        y = temp;
        System.out.println("End of method: x = " + x.getName());
        System.out.println("End of method: y = " + y.getName());
    }
}

class Employee  // simplified Employee class
{
    private String name;
    private double salary;

    public Employee(String n, double s)
    {
        name = n;
        salary = s;
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
}
```

关于重载的代码示例

> ConstructorTest.java

```java
package ConstructorTest;

import java.util.*;

public class ConstructorTest {
    public static void main(String[] args)
    {
        // fill the staff array with three Employee objects
        Employee[] staff = new Employee[3];

        staff[0] = new Employee("Harry", 40000);
        staff[1] = new Employee(60000);
        staff[2] = new Employee();

        // print out information about all Employee objects
        for (Employee e : staff)
        {
            System.out.println("name = " + e.getName() + ", id = " + e.getId() + ", salary = " + e.getSalary());
        }
    }
}

class Employee
{
    private static int nextId;

    private int id;
    private String name = "";  // instance field initialization
    private double salary;

    // static initialization block
    // 静态属性的初始化区域，想要给静态属性初始化就用这样的块 statid{ TODO; }
    static
    {
        Random generator = new Random();
        // set nextId to a random number between 0 and 9999
        nextId = generator.nextInt(10000);
    }

    // object initialization block
    // 也可以在这里初始化非静态的属性，这个代码块的优点就是可以写代码，进行一些运算，然后赋值
    {
        id = nextId;
        nextId++;
    }

    // three overloaded constructors
    // 有多个构造方法就叫重载
    public Employee(String n, double s)
    {
        name = n;
        salary = s;
    }

    public Employee(double s)
    {
        // calls the Employee(String , double) constructor
        // 使用this（）来调用其他的构造方法
        this("Employee #"+ nextId, s);
    }

    // the default constructor
    public Employee()
    {
        // name initialized to "" --see above
        // salary not explicitly set--initialized to 0
        // id initialized in initialization block
    }

    public String getName()
    {
        return name;
    }

    public double getSalary()
    {
        return salary;
    }

    public int getId()
    {
        return id;
    }
}
```

关于包和导入的代码示例

> PackageTest.java

```java
package PackageTest;

// 导入包，一般在使用其他文件里的类的时候是需要导入类
import PackageTest.cc.singll.learnjava.Employee;

// 也可以导入类所在的包，这样就可以使用这个包里的所有类，比如这里的System，用*表示包下的所有类， static 的意思是导入静态的方法和静态的属性，这样就可以不用加类名了，直接当作在本类里的方法一样调用
import static java.lang.System.*;

public class PackageTest {
    public static void main(String[] args)
    {
        // because of the import statement, we don't have to use
        // PackageTest.cc.singll.learnjava.Employee here
        Employee harry = new Employee("Harry Hacker", 50000, 1989, 10, 1);

        harry.raiseSalary(5);

        // because of the static import statement, we don't hava to use System.out here
        out.print("name = " + harry.getName() + ", salary = " + harry.getSalary());
    }
}
```

> Employee.java

```java
package PackageTest.cc.singll.learnjava;
// 包名，这里的包要和物理路径对应上，比如 此文件的物理路径就是 PackageTest/cc/singll/learnjava/Employee.java

import java.time.*;

// 这里将类分开了，其他的类里想用Employee的类，直接导入类，就可以使用了
public class Employee {
    private String name;
    private double salary;
    private LocalDate hireDay;

    public Employee(String name, double salary, int year, int month, int day)
    {
        this.name = name;
        this.salary = salary;
        hireDay = LocalDate.of(year, month, day);
    }

    public String getName()
    {
        return name;
    }

    public double getSalary()
    {
        return salary;
    }

    public LocalDate getHireDay()
    {
        return hireDay;
    }

    public void raiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }
}

```
# 0x03
    拖了一周，不过总算是补回来了，这里的光看文章会看不懂，要结合书来看，这里只是大致讲一下，毕竟还是书里讲的最好
