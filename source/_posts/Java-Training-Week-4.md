---
title: '[Java Training]Week 4'
date: 2019-08-17 22:15:10
categories: Java
tags: Java
index_img: https://i.loli.net/2019/07/07/5d21cd23675da29020.jpg
---
# 0x00
    本系列-Java集训系列
    记录我带领小组进行Java学习，按照《Java核心技术》第十版进行学习
# 0x01
    继承
# 0x02
1. 子类和父类：父类就是正常的类，子类是继承父类的方法和属性，可以继承public与protected
2. super：在子类可以使用super()来调用父类的构造方法，也可以用super.method()调用父类的方法

> ManagerTest.java

```java
package cc.singll.learnjava.inheritance;

public class ManagerTest {
    public static void main(String[] args)
    {
        Manager boss = new Manager("Carl Cracker", 80000, 1987, 12, 15);
        boss.setBonus(5000);
        Employee[] staff = new Employee[3];

        // fill the staff array with Manager and Employee objects

        staff[0] = boss;
        staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
        staff[2] = new Employee("Tommy Tester", 40000, 1990, 3, 15);

        //print out information about all Employee objects
        for (Employee e : staff)
            System.out.println("name=" + e.getName() + ", salary=" + e.getSalary());
    }
}
```

> Employee.java

```java
package cc.singll.learnjava.inheritance;

import java.time.*;

// 父类 正常的类，可以被继承
public class Employee {

    // 私有属性不可以被继承
    private String name;
    private double salary;
    private LocalDate hireDay;

    public Employee(String name, double salary, int year, int month, int day)
    {
        this.name = name;
        this.salary = salary;
        hireDay = LocalDate.of(year, month, day);
    }

    // 公共方法可以被继承
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

    public void ralseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }
}

```

> Manager.java

```java
package cc.singll.learnjava.inheritance;

// 使用extends关键字表示继承，extends 后面跟着的是继承的父类
public class Manager extends Employee {
    private double bonus;

    public Manager(String name, double salary, int year, int month, int day)
    {
        // 使用super调用父类的构造方法
        super(name, salary, year, month, day);
        bonus = 0;
    }

    public double getSalary()
    {
        // 使用super.method() 调用父类的方法
        double baseSalary = super.getSalary();
        return baseSalary + bonus;
    }

    public void setBonus(double b)
    {
        bonus = b;
    }
}

```

1. 多态：简单理解就是子类以及子类的子类可以使用父类的类型声明的变量来存放，并且可以使用这个变量来进行方法调用等操作
2. final：在类声明的时候使用了final修饰符，则表示此类不可以被继承，即不会有子类
3. 父类的引用赋给子类的变量，则需要强制类型转换
4. 抽象类：使用abstract修饰符修饰类，或者使用abstract修饰类里的方法，则为抽象类，抽象类不可以实例化对象，并且抽象修饰的方法，子类必须实现或者将自身声明为抽象方法留给子类实现，即抽象方法是子类必定存在的方法，并且会有不同实现

> PersonTest.java

```java
package cc.singll.learnjava.abstractClasses;

public class PersonTest {
    public static void main(String[] args)
    {
        Person[] people = new Person[2];

        // fill the people array with Student and Employee objects
        // 声明为Person类型，但是可以将子类的对象放进去
        people[0] = new Employee("Harry Hacker", 40000, 1989, 10, 1);
        people[1] = new Student("Maria Morris", "computer scrience");

        // print out names and descriptions of all Person objects
        for (Person p : people)
        {
            // 并且可以通过父类的类型变量来调用子类的方法
            System.out.println(p.getName() + ", " + p.getDescription());
        }
    }
}

```

> Person.java

```java
package cc.singll.learnjava.abstractClasses;

// 使用abstract修饰类，表示是抽象类
public abstract class Person {

    // 使用abstract修饰的方法是抽象方法，抽象方法不可以有具体代码，只能声明，子类如果继承之后，有两个选择，一是实现所有抽象方法（即里面包含具体代码），二是继续保留抽象方法，则类也必须是抽象类
    public abstract String getDescription();
    private String name;

    // 抽象类里可以有正常方法
    public Person(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }
}

```

> Employee.java

```java
package cc.singll.learnjava.abstractClasses;

import java.time.*;

public class Employee extends Person {
    private double salary;
    private LocalDate hireDay;

    public Employee(String name, double salary, int year, int month, int day)
    {
        super(name);
        this.salary = salary;
        hireDay = LocalDate.of(year, month, day);
    }

    public double getSalary()
    {
        return salary;
    }

    public LocalDate getHireDay()
    {
        return hireDay;
    }

    // 实现了抽象类
    public String getDescription()
    {
        return String.format("An employee with a salary of $%.2f", salary);
    }

    public void reiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }
}

```

> Student.java

```java
package cc.singll.learnjava.abstractClasses;

public class Student extends Person {
    private String major;

    public Student(String name, String major)
    {
        super(name);
        this.major = major;
    }

    // 实现了抽象类
    public String getDescription()
    {
        return "a student majoring in " + major;
    }
}

```

1. Object： Object是所有类的父类，即除了基本类型，其他类或是子类的子类，如果没有声明是其他类的子类，那么就是Object的子类
2. equals：Object类方法，用来判断两个类是否相等，Object里的实现是判断两个类是否是同一个引用，自定义类可以通过重写equals方法来进行定制的相等判定
3. hashCode：Object类方法，返回一个int型的散列码
4. toString：Object类方法，返回表示对象值的字符串

> EqualsTest.java

```java
package cc.singll.learnjava.equals;

public class EqualsTest {
    public static void main(String[] args)
    {
        Employee alice1 = new Employee("Alice Adams", 75000, 1987, 12, 15);
        Employee alice2 = alice1;
        Employee alice3 = new Employee("Alice Adams", 75000, 1987, 12, 15);
        Employee bob = new Employee("Bob Brandson", 50000, 1989, 10, 1);

        System.out.println("alice1 == alice2: " + (alice1 == alice2));

        System.out.println("alice1 == alice3: " + (alice1 == alice3));

        System.out.println("alice1.equals(alice3): " + alice1.equals(alice3));

        System.out.println("bob.toString(): " + bob);

        Manager carl = new Manager("Carl Cracker", 80000, 1987, 12, 15);
        Manager boss = new Manager("Carl Cracker", 80000, 1987, 12, 15);
        boss.setBonus(5000);
        System.out.println("boss.toString(): " + boss);
        System.out.println("carl.equals(boss): " + carl.equals(boss));
        System.out.println("alice1.hashCode(): " + alice1.hashCode());
        System.out.println("alice3.hashCode(): " + alice3.hashCode());
        System.out.println("bob.hashCode(): " + bob.hashCode());
        System.out.println("carl.hashCode(): " + carl.hashCode());
    }
}

```

> Employee.java

```java
package cc.singll.learnjava.equals;

import java.time.*;
import java.util.Objects;

// 默认继承Object类
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

    // 重写的equals方法
    public boolean equals(Object otherObject)
    {
        // a quick test to see if the objects are identical
        if (this == otherObject) return true;

        // must return false if the explicit parameter is null
        if (getClass() != otherObject.getClass()) return false;

        // now we know otherObject is a non-null Employee
        Employee other = (Employee) otherObject;

        // test whether the fields have identical values
        return Objects.equals(name, other.name) && salary == other.salary && Objects.equals(hireDay, other.hireDay);
    }

    // 重写的hashCOde方法
    public int hashCode()
    {
        return Objects.hash(name, salary, hireDay);
    }

    // 重写的toString方法
    public String toString()
    {
        return getClass().getName() + "[name=" + name + ", salary=" + salary + ",hireDay=" + hireDay + "]";
    }
}

```

> Manager.java

```java
package cc.singll.learnjava.equals;

public class Manager extends Employee {
    private double bonus;

    public Manager(String name, double salary, int year, int month, int day)
    {
        super(name, salary, year, month, day);
        bonus = 0;
    }

    public double getSalary()
    {
        double baseSalary = super.getSalary();
        return baseSalary + bonus;
    }

    public void setBonus(double bonus)
    {
        this.bonus = bonus;
    }

    // 重写equals方法
    public boolean equals(Object otherObject)
    {
        if (!super.equals(otherObject)) return false;
        Manager other = (Manager) otherObject;
        // super.equals checked that this and other belong to the same class
        return bonus == other.bonus;
    }

    // 重写hashCode方法
    public int hashCode()
    {
        return super.hashCode() + 17 * new Double(bonus).hashCode();
    }

    // 重写toString方法
    public String toString()
    {
        return getClass().getName() + "[bonus=" + bonus + "]";
    }
}

```

1. 泛型数组列表：数量可变的数组，使用方式为ArrayList<Object>，而且，赋值、取值等操作都是用的另一套方法，请看下面代码

> ArrayListTest.java

```java
package cc.singll.learnjava.arrayList;

import java.util.*;
import cc.singll.learnjava.equals.Employee;

public class ArrayListTest {
    public static void main(String[] args)
    {
        // fill the staff array list with three Employee objects
        // 定义Employee类型的数组
        ArrayList<Employee> staff = new ArrayList<>();

        // 添加元素使用.add()
        staff.add(new Employee("Carl Cracker", 75000, 1987, 12, 15));
        staff.add(new Employee("Harry Hacker", 50000, 1989, 10, 1));
        staff.add(new Employee("Tony Tester", 40000, 1990, 3, 15));

        // raise everyone's salary by 5%
        // 可以对泛型数组列表进行遍历
        for (Employee e : staff)
        {
            e.raiseSalary(5);
        }

        // print out information about all Employee objects
        for (Employee e : staff)
        {
            System.out.println("name=" + e.getName() + ",salary=" + e.getSalary() + ",hireDay=" + e.getHireDay());
        }
    }
}

```

1. 对象包装器：首先，ArrayList<Object> 的Object必须是对象，但是当想要使用基本类型的时候，是不可以直接放进去的，这就可以用对象包装器，每个基本类型都有一个对应的对象版本，Integer、Long、Float、Double、Short、Byte、Character、Void、Boolean。对象包装器类是不可变的，即一旦构造了包装器，就不允许更改包装再其中的值。同时，对象包装器类还是final，因此不能定义他们的子类。
2. 参数数量可变：定义参数可变的形式(Object... args)，这样可以接收任意多的参数
3. 枚举类：看下面代码

> EnumTest.java

```java
package cc.singll.learnjava.enums;

import java.util.*;

public class EnumTest {
    public static void main(String[] args)
    {
        Scanner in = new Scanner(System.in);
        System.out.println("Enter a size: (SMALL, MEDIUM, LARGE, EXTRA_LARGE) ");
        String input = in.next().toUpperCase();
        Size size = Enum.valueOf(Size.class, input);
        System.out.println("size=" + size);
        System.out.println("abbreviation=" + size.getAbbreviation());
        
        // Size.EXTRA_LARGE是使用方法，值就是""中定义的
        if (size == Size.EXTRA_LARGE)
            System.out.println("Good job--you paid attention to the _.");
    }
}

// 定义枚举类，叫做Size
enum Size
{
    // 定义使用的名称和对应的值
    SMALL("S"),MEDIUM("M"),LARGE("L"),EXTRA_LARGE("XL");

    // 也可以在枚举类里使用构造方法和方法，还有属性
    private Size(String abbreviation) { this.abbreviation = abbreviation;}
    public String getAbbreviation() { return abbreviation;}

    private String abbreviation;
}

```

反射
1. Class类：在程序运行期间，Java运行时系统为所有的对象维护一个跟踪每个类信息标识，就是Class类，通过Object类中的getClass()方法可以获得一个对象的Class类型的实例
2. 通过这个Class类型的实例，可以进行创建对象，获得类方法、属性、构造方法

> ReflectionTest.java

```java
package cc.singll.learnjava.reflection;

import java.util.*;
import java.lang.reflect.*;

public class ReflectionTest {
    public static void main(String[] args)
    {
        // read class name from command line args or user input
        String name;
        if (args.length > 0) name = args[0];
        else
        {
            Scanner in = new Scanner(System.in);
            System.out.println("Enter class name (e.g. java.util.Date): ");
            name = in.next();
        }

        try
        {
            // print class name and superclass name (if != Object)
            // 通过Class.forName(name)来获取类的Class实例
            Class cl = Class.forName(name);
            // 通过Class.getSuperclass()获得父类
            Class supercl = cl.getSuperclass();
            // 通过Class.getModifiers() 获得类修饰符的数值，然后通过toString变成字符串
            String modifiers = Modifier.toString(cl.getModifiers());
            if (modifiers.length() > 0) System.out.print(modifiers + " ");
            System.out.print("class " + name);
            if (supercl != null && supercl != Object.class) System.out.print(" extends " + supercl.getName());
            System.out.print("\n{\n");
            printConstructors(cl);
            System.out.println();
            printMethods(cl);
            System.out.println();
            printFields(cl);
            System.out.println("}");
        }
        catch (ClassNotFoundException e)
        {
            e.printStackTrace();
        }
        System.exit(0);
    }

    public static void printConstructors(Class cl)
    {
        Constructor[] constructors = cl.getDeclaredConstructors();
        for (Constructor c : constructors)
        {
            String name = c.getName();
            System.out.print("    ");
            String modifiers = Modifier.toString(c.getModifiers());
            if (modifiers.length() > 0) System.out.print(modifiers + " ");
            System.out.print(name + "(");

            // print parameter types
            Class[] paramTypes = c.getParameterTypes();
            for (int j = 0; j < paramTypes.length; j++)
            {
                if (j > 0) System.out.print(", ");
                System.out.print(paramTypes[j].getName());
            }
            System.out.println(");");
        }
    }

    public static void printMethods(Class cl)
    {
        Method[] methods = cl.getDeclaredMethods();

        for (Method m : methods)
        {
            Class retType = m.getReturnType();
            String name = m.getName();

            System.out.print("    ");
            // print modifiers, return type and method name
            String modifiers = Modifier.toString(m.getModifiers());
            if (modifiers.length() > 0) System.out.print(modifiers + " ");
            System.out.print(retType.getName() + " " + name + "(");
            // print parameter types
            Class[] paramTypes = m.getParameterTypes();
            for (int j = 0; j < paramTypes.length; j++)
            {
                if (j > 0) System.out.print(", ");
                System.out.print(paramTypes[j].getName());
            }
            System.out.println(");");
        }
    }

    public static void printFields(Class cl)
    {
        Field[] fields = cl.getDeclaredFields();

        for (Field f : fields)
        {
            Class type = f.getType();
            String name = f.getName();
            System.out.print("    ");
            String modifiers = Modifier.toString(f.getModifiers());
            if (modifiers.length() > 0) System.out.print(modifiers + " ");
            System.out.println(type.getName() + " " + name + ";");
        }
    }
}

```

上面的代码遇到private的会报错，下面的代码可以将所有的属性设置成public，然后获取值

> ObjectAnalyzerTest.java

```java
package cc.singll.learnjava.objectAnalyzer;

import java.util.ArrayList;

public class ObjectAnalyzerTest {
    public static void main(String[] args)
    {
        ArrayList<Integer> squares = new ArrayList<>();
        for (int i = 1; i <= 5; i++)
        {
            squares.add(i * i);
        }
        System.out.println(new ObjectAnalyzer().toString(squares));
    }
}

```

> ObjectAnalyzer.java

```java
package cc.singll.learnjava.objectAnalyzer;

import java.lang.reflect.AccessibleObject;
import java.lang.reflect.Array;
import java.lang.reflect.Field;
import java.lang.reflect.Modifier;
import java.util.ArrayList;

public class ObjectAnalyzer {
    private ArrayList<Object> visited = new ArrayList<>();

    public String toString(Object obj)
    {
        if (obj == null) return "null";
        if (visited.contains(obj)) return "...";
        visited.add(obj);
        Class cl = obj.getClass();
        if (cl == String.class) return (String)obj;
        if (cl.isArray())
        {
            String r = cl.getComponentType() + "[]{";
            for (int i = 0; i < Array.getLength(obj); i++)
            {
                if (i > 0) r += ",";
                Object val = Array.get(obj, i);
                if (cl.getComponentType().isPrimitive()) r += val;
                else r += toString(val);
            }
            return r + "}";
        }

        String r = cl.getName();
        // inspect the fields of this class and all superclasses
        do
        {
            r +="{";
            Field[] fields = cl.getDeclaredFields();
            // 调用.setAccessible()
            AccessibleObject.setAccessible(fields, true);
            // get the names and values of all fields
            for (Field f : fields)
            {
                if (!Modifier.isStatic(f.getModifiers()))
                {
                    if (!r.endsWith("[")) r += ",";
                    r += f.getName() + "=";
                    try
                    {
                        Class t = f.getType();
                        Object val = f.get(obj);
                        if (t.isPrimitive()) r += val;
                        else r += toString(val);
                    }
                    catch (Exception e)
                    {
                        e.printStackTrace();
                    }
                }
            }
            r += "]";
            cl = cl.getSuperclass();
        }
        while (cl != null);
        return r;
    }
}

```

下面代码是演示怎么运行时创建一个新数组，然后从旧数组复制过来

> CopyOfTest.java

```java
package cc.singll.learnjava.arrays;

import java.lang.reflect.*;
import java.util.*;

public class CopyOfTest {
    public static void main(String[] args)
    {
        int[] a = {1, 2, 3};
        a = (int[]) goodCopyOf(a, 10);
        System.out.println(Arrays.toString(a));

        String[] b = {"Tom", "Dick", "Harry"};
        b = (String[]) goodCopyOf(b, 10);
        System.out.println(Arrays.toString(b));

        System.out.println("The following call will generate an exception.");
        b = (String[]) badCopyOf(b, 10);
    }

    // 错误的方法，不可以用Object来转成其他类型
    public static Object[] badCopyOf(Object[] a, int newLength) // not useful
    {
        Object[] newArray = new Object[newLength];
        System.arraycopy(a, 0, newArray, 0, Math.min(a.length, newLength));
        return newArray;
    }

    // 正确的方法，先使用.getClass()来获取类，然后用获取到的类来创建新的对象
    public static Object goodCopyOf(Object a, int newLength)
    {
        Class cl = a.getClass();
        if (!cl.isArray()) return null;
        Class componentType = cl.getComponentType();
        int length = Array.getLength(a);
        Object newArray = Array.newInstance(componentType, newLength);
        System.arraycopy(a, 0, newArray, 0, Math.min(length, newLength));
        return newArray;
    }
}

```

反射可以调用任意方法

> MethodTableTest.java

```java
package cc.singll.learnjava.methods;

import java.lang.reflect.*;

public class MethodTableTest {
    public static void main(String[] args) throws Exception
    {
        // get method pointers to the square and sqrt methods
        Method square = MethodTableTest.class.getMethod("square", double.class);
        Method sqrt = Math.class.getMethod("sqrt", double.class);

        // print tables of x- and y-values

        printTable(1, 10, 10, square);
        printTable(1, 10, 10, sqrt);

    }

    public static double square(double x)
    {
        return x * x;
    }

    public static void printTable(double from, double to, int n, Method f)
    {
        System.out.println(f);
        double dx = (to - from) / (n - 1);
        for (double x = from; x <= to; x += dx)
        {
            try
            {
                // 使用.invoke来进行调用方法（与普通的调用不同的是这是运行时调用，即可变的，而普通的是在编译时就已经确定下来)
                double y = (Double) f.invoke(null, x);
                System.out.printf("%10.4f | %10.4f%n", x, y);
            }
            catch (Exception e)
            {
                e.printStackTrace();
            }
        }
    }
}

```

可以看到反射是很强大的，也是很危险的（破坏封装），如果写应用会很少用到，但是写工具会大量用到
尤其是，反序列化漏洞会用到