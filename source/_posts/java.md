# 1 基本语法

## 1.1 String

在Java中，`String` 类是用于表示字符串的类，它提供了丰富的方法和功能来操作字符串。字符串是一组字符的序列，而在Java中，字符串是不可变的，这意味着一旦创建了字符串，就不能更改其内容。

以下是一些常用的 `String` 类的用法和示例：

### 1. 创建字符串

可以通过直接赋值或使用构造函数创建字符串对象：

```java
String str1 = "Hello, World!";  // 使用直接赋值创建字符串
String str2 = new String("Hello, World!");  // 使用构造函数创建字符串
```

### 2. 获取字符串长度

可以使用 `length()` 方法获取字符串的长度：

```java
String str = "Hello, World!";
int length = str.length();  // 获取字符串长度
System.out.println("Length of the string: " + length);
```

### 3. 拼接字符串

可以使用 `+` 运算符或 `concat()` 方法将多个字符串拼接在一起：

```java
String str1 = "Hello, ";
String str2 = "World!";
String result = str1 + str2;  // 使用 + 运算符拼接字符串
// 或者使用 concat() 方法
String result = str1.concat(str2);
System.out.println("Concatenated string: " + result);
```

### 4. 字符串比较

可以使用 `equals()` 方法或 `compareTo()` 方法比较字符串：

```java
String str1 = "hello";
String str2 = "Hello";
boolean isEqual = str1.equals(str2);  // 使用 equals() 比较字符串
int comparison = str1.compareTo(str2);  // 使用 compareTo() 比较字符串
```

### 5. 提取子字符串

可以使用 `substring()` 方法从字符串中提取子串：

```java
String str = "Hello, World!";
String subStr = str.substring(7);  // 提取从位置7开始的子串
System.out.println("Substring: " + subStr);
```

### 6. 查找子字符串

可以使用 `indexOf()` 方法或 `contains()` 方法查找子字符串是否存在：

```java
String str = "Hello, World!";
int index = str.indexOf("World");  // 查找子串的位置
boolean contains = str.contains("Hello");  // 检查是否包含子串
```

## 1.2 StringBuilder 

在Java中，`StringBuilder` 是一个用于处理可变字符串的类。与 `String` 不同，`StringBuilder` 允许你在不创建新对象的情况下修改字符串的内容，这对于频繁的字符串拼接操作非常高效。以下是一些使用 `StringBuilder` 的常见方法和示例：

### 1. 创建 `StringBuilder` 对象

可以使用构造函数创建一个 `StringBuilder` 对象：

```java
StringBuilder sb = new StringBuilder(); // 创建一个空的 StringBuilder 对象
```

你也可以在构造函数中传入一个初始字符串：

```java
StringBuilder sb = new StringBuilder("Hello"); // 创建包含初始字符串 "Hello" 的 StringBuilder 对象
```

### 2. 追加字符串

可以使用 `append()` 方法来追加字符串到 `StringBuilder` 对象：

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(", World!"); // 追加字符串
```

### 3. 插入字符串

使用 `insert()` 方法可以在指定位置插入字符串：

```java
StringBuilder sb = new StringBuilder("Hello");
sb.insert(5, " Java"); // 在位置5插入字符串
```

### 4. 删除字符

使用 `delete()` 方法可以删除指定范围内的字符：

```java
StringBuilder sb = new StringBuilder("Hello, World!");
sb.delete(7, 13); // 删除位置7到13之间的字符
```

### 5. 替换字符

使用 `replace()` 方法可以替换指定范围内的字符：

```java
StringBuilder sb = new StringBuilder("Hello, World!");
sb.replace(7, 13, "Java"); // 将位置7到13之间的字符替换为 "Java"
```

### 6. 获取字符串

使用 `toString()` 方法可以将 `StringBuilder` 对象转换为 `String`：

```java
StringBuilder sb = new StringBuilder("Hello, World!");
String result = sb.toString(); // 转换为 String
```

### 7. 获取长度

可以使用 `length()` 方法获取 `StringBuilder` 中字符的数量：

```java
StringBuilder sb = new StringBuilder("Hello, World!");
int length = sb.length(); // 获取长度
```

`StringBuilder` 的方法允许你执行许多字符串操作，而不需要创建多个不必要的字符串对象，这在性能上通常更高效。因此，当需要频繁修改字符串时，建议使用 `StringBuilder`。

## 1.3 final关键字

`final` 是 Java 编程语言中的一个关键字，用于表示不可变性和不可继承性，它可以用于不同的上下文中，具体作用如下：

1. **不可变变量**：当你将 `final` 关键字应用于一个变量时，它表示该变量的值不能被修改，即它是一个不可变变量（immutable）。通常用于声明常量，这意味着一旦分配了值，就不能再更改。例如：

   ```java
   final int x = 10;
   // x = 20;  // 这将导致编译错误，因为 x 是不可变的
   ```

2. **不可变类**：当你将 `final` 关键字应用于一个类时，它表示该类不能被继承，即它是一个不可继承的类。这通常用于防止其他类继承或修改基类的行为，以确保类的稳定性和安全性。

   ```java
   final class MyFinalClass {
       // 类的成员和方法
   }
   // 下面的代码将导致编译错误，因为无法继承 MyFinalClass
   // class AnotherClass extends MyFinalClass { ... }
   ```

3. **不可变方法**：当你将 `final` 关键字应用于一个方法时，它表示该方法不能被子类重写或覆盖。这通常用于确保某个方法的行为不会被修改。

   ```java
   class MyBaseClass {
       final void myFinalMethod() {
           // 这个方法不能被子类重写
       }
   }
   ```

4. **不可变参数**：当你将 `final` 关键字应用于方法的参数时，它表示该参数的值在方法内部不能被修改。

   ```java
   void myMethod(final int param) {
       // param 的值不能在方法内部被修改
   }
   ```

## 1.4 super关键字

`super` 是 Java 中的一个关键字，用于引用父类（或超类）的成员变量、方法和构造函数。它可以在子类中使用，用于访问或调用父类的成员或构造函数。以下是关于 `super` 关键字的使用方法：

1. **访问父类的成员变量**：你可以使用 `super` 关键字来访问父类中的成员变量，特别是在子类中存在与父类同名的成员变量时。这样可以避免混淆。

   ```java
   class Parent {
       int x = 10;
   }
   
   class Child extends Parent {
       int x = 20;
   
       void display() {
           System.out.println("子类 x：" + x); // 访问子类的 x
           System.out.println("父类 x：" + super.x); // 访问父类的 x
       }
   }
   ```

2. **调用父类的方法**：你可以使用 `super` 关键字来调用父类中的方法，特别是在子类中存在与父类同名的方法时。

   ```java
   class Parent {
       void showMessage() {
           System.out.println("这是父类的消息");
       }
   }
   
   class Child extends Parent {
       void showMessage() {
           System.out.println("这是子类的消息");
           super.showMessage(); // 调用父类的 showMessage() 方法
       }
   }
   ```

3. **调用父类的构造函数**：你可以使用 `super` 关键字来调用父类的构造函数。这通常用于子类的构造函数中，以确保父类的初始化工作得以执行。

   ```java
   class Parent {
       Parent() {
           System.out.println("父类的构造函数");
       }
   }
   
   class Child extends Parent {
       Child() {
           super(); // 调用父类的构造函数
           System.out.println("子类的构造函数");
       }
   }
   ```

注意事项：

- 在子类构造函数中，如果没有显式调用 `super()` 来调用父类的构造函数，Java 将自动调用父类的默认构造函数。
- `super()` 必须作为子类构造函数的第一行语句出现，因此它通常是构造函数的第一句。

## 1.5 abstract 关键字

`abstract` 是 Java 中的一个关键字，用于声明抽象类和抽象方法。抽象类和抽象方法的目的是为了提供一种结构，以便其他类可以继承或实现它们，并根据需要进行定制化实现。以下是 `abstract` 关键字的主要作用：

1. **抽象类**：

   - 抽象类用 `abstract` 关键字声明，它不能被实例化（不能创建对象）。
   - 抽象类可以包含抽象方法和非抽象方法。
   - 抽象类的存在是为了被继承和拓展，提供通用的结构和行为。

   ```java
   abstract class AbstractClass {
       // 抽象方法
       abstract void abstractMethod();
   
       // 普通方法
       void nonAbstractMethod() {
           System.out.println("非抽象方法的实现");
       }
   }
   ```

2. **抽象方法**：

   - 抽象方法用 `abstract` 关键字声明，但没有方法体。
   - 抽象方法必须在抽象类中声明，不允许在普通类中声明。
   - 抽象方法的具体实现由继承抽象类的子类完成。

   ```java
   abstract class AbstractClass {
       // 抽象方法
       abstract void abstractMethod();
   }
   
   class ConcreteClass extends AbstractClass {
       // 必须实现抽象方法
       @Override
       void abstractMethod() {
           System.out.println("抽象方法的实现");
       }
   }
   ```

抽象类和抽象方法的作用是为了促使子类实现特定的行为，同时确保了基类中的通用结构。这有助于提高代码的可维护性和扩展性，同时强调了面向对象设计的抽象思想。

# 2 类

## 2.1 接口

在 Java 中，接口（Interface）是一种抽象类型，它定义了一组抽象方法，但没有具体的实现。接口通常用于描述对象应该具有的行为。以下是关于 Java 接口的主要特点：

1. **接口定义**：接口使用 `interface` 关键字定义。

   ```java
   interface MyInterface {
       // 抽象方法的声明
       void abstractMethod();
   }
   ```

2. **抽象方法**：接口中的方法都是抽象的，它们只有方法签名，没有方法体。

3. **接口实现**：一个类可以实现一个或多个接口。使用关键字 `implements` 来表示类实现了一个接口。

   ```java
   class MyClass implements MyInterface {
       // 必须实现接口中的抽象方法
       @Override
       public void abstractMethod() {
           // 实现具体逻辑
       }
   }
   ```

4. **多继承**：Java 中不支持多继承，但一个类可以实现多个接口，这使得 Java 中的多继承概念得以体现。

   ```java
   interface Interface1 {
       void method1();
   }
   
   interface Interface2 {
       void method2();
   }
   
   class MyClass implements Interface1, Interface2 {
       @Override
       public void method1() {
           // 实现 method1
       }
   
       @Override
       public void method2() {
           // 实现 method2
       }
   }
   ```

5. **接口默认方法**：从 Java 8 开始，接口可以包含具有默认实现的方法。

   ```java
   interface MyInterface {
       void abstractMethod();
   
       default void defaultMethod() {
           System.out.println("默认方法的实现");
       }
   }
   ```

6. **接口静态方法**：从 Java 8 开始，接口可以包含静态方法。

   ```java
   interface MyInterface {
       void abstractMethod();
   
       static void staticMethod() {
           System.out.println("静态方法的实现");
       }
   }
   ```

接口在 Java 中扮演着重要的角色，它提供了一种将抽象概念定义为一组行为的方式，从而实现了多态性和代码复用。接口也是 Java 中实现多继承的一种方式，使得类可以实现多个行为规范。

## 2.2 @Override

`@Override` 注解用于告诉编译器，被标注的方法是要重写（覆盖）父类或接口中的方法。通常情况下，你应该在以下情况下使用 `@Override` 注解：

1. **重写父类方法**：当你在子类中编写一个方法，其名称、参数列表和返回类型与父类中的方法完全一致时，应该使用 `@Override` 注解来明确指示你意图重写父类方法。

   ```java
   class Parent {
       void myMethod() {
           // 父类方法
       }
   }
   
   class Child extends Parent {
       @Override
       void myMethod() {
           // 子类重写的方法
       }
   }
   ```

2. **实现接口方法**：当你在一个类中实现了一个接口中的方法时，也应该使用 `@Override` 注解。这有助于提醒你，你是在实现一个接口方法，而不是创建一个新的方法。

   ```java
   interface MyInterface {
       void myMethod();
   }
   
   class MyClass implements MyInterface {
       @Override
       public void myMethod() {
           // 实现接口方法
       }
   }
   ```

3. **编码规范**：在许多编码规范中，推荐使用 `@Override` 注解，以提高代码的可读性和可维护性。这有助于其他开发人员理解你的代码意图，并防止意外的方法签名变更。

虽然在上述情况下使用 `@Override` 注解是很好的实践，但并非所有情况下都需要使用它。在以下情况下，你通常不需要使用 `@Override` 注解：

- 当你编写的方法不是为了重写父类或实现接口中的方法时。
- 当你在 Java 版本低于 5 的环境中编写代码，因为 `@Override` 注解是在 Java 5 中引入的。

# 3 常用类

## 3.1 Arrays

当使用 `Arrays` 类的方法时，通常需要导入 `java.util.Arrays` 包。以下是一些使用 `Arrays` 类方法的示例：

**1. 使用 `sort` 方法对数组进行排序：**

```java
import java.util.Arrays;

public class ArraySortingExample {
    public static void main(String[] args) {
        int[] numbers = {5, 2, 9, 1, 5, 6};
        
        Arrays.sort(numbers);
        
        System.out.println("Sorted Array: " + Arrays.toString(numbers));
    }
}
```

**2. 使用 `binarySearch` 方法查找元素：**

```java
import java.util.Arrays;

public class BinarySearchExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5, 6};
        
        int key = 3;
        int index = Arrays.binarySearch(numbers, key);
        
        if (index >= 0) {
            System.out.println("Element " + key + " found at index " + index);
        } else {
            System.out.println("Element " + key + " not found in the array");
        }
    }
}
```

**3. 使用 `equals` 方法比较数组：**

```java
import java.util.Arrays;

public class ArrayComparisonExample {
    public static void main(String[] args) {
        int[] array1 = {1, 2, 3};
        int[] array2 = {1, 2, 3};
        
        boolean isEqual = Arrays.equals(array1, array2);
        
        if (isEqual) {
            System.out.println("Arrays are equal.");
        } else {
            System.out.println("Arrays are not equal.");
        }
    }
}
```

**4. 使用 `fill` 方法填充数组：**

```java
import java.util.Arrays;

public class ArrayFillExample {
    public static void main(String[] args) {
        int[] numbers = new int[5];
        
        Arrays.fill(numbers, 42);
        
        System.out.println("Filled Array: " + Arrays.toString(numbers));
    }
}
```

## 3.2 time

`java.time` 包是Java 8引入的现代日期和时间处理API，提供了一系列类来处理日期、时间和时区。以下是一些`java.time`包的主要类和用法示例：

1. **LocalDate**：用于表示日期，不包含时间和时区信息。

   ```java
   LocalDate today = LocalDate.now();
   LocalDate customDate = LocalDate.of(2023, 9, 25);
   
   int year = today.getYear();
   int month = today.getMonthValue();
   int day = today.getDayOfMonth();
   ```

2. **LocalTime**：用于表示时间，不包含日期和时区信息。

   ```java
   LocalTime currentTime = LocalTime.now();
   LocalTime customTime = LocalTime.of(14, 30, 0);
   
   int hour = currentTime.getHour();
   int minute = currentTime.getMinute();
   int second = currentTime.getSecond();
   ```

3. **LocalDateTime**：用于表示日期和时间的组合，不包含时区信息。

   ```java
   LocalDateTime currentDateTime = LocalDateTime.now();
   LocalDateTime customDateTime = LocalDateTime.of(2023, 9, 25, 14, 30, 0);
   
   int year = currentDateTime.getYear();
   int month = currentDateTime.getMonthValue();
   int hour = currentDateTime.getHour();
   ```

4. **ZonedDateTime**：用于表示带时区的日期和时间。

   ```java
   ZoneId newYorkZone = ZoneId.of("America/New_York");
   ZonedDateTime newYorkTime = ZonedDateTime.now(newYorkZone);
   
   ZoneId londonZone = ZoneId.of("Europe/London");
   ZonedDateTime londonTime = newYorkTime.withZoneSameInstant(londonZone);
   ```

5. **Duration**：用于表示时间段，可以用于计算时间间隔。

   ```java
   LocalDateTime start = LocalDateTime.of(2023, 9, 1, 8, 0);
   LocalDateTime end = LocalDateTime.of(2023, 9, 5, 17, 0);
   Duration duration = Duration.between(start, end);
   
   long hours = duration.toHours();
   long minutes = duration.toMinutes();
   ```

6. **Period**：用于表示日期段，可以用于计算日期间隔。

   ```java
   LocalDate startDate = LocalDate.of(2023, 9, 1);
   LocalDate endDate = LocalDate.of(2023, 9, 5);
   Period period = Period.between(startDate, endDate);
   
   int days = period.getDays();
   int months = period.getMonths();
   ```

7. **DateTimeFormatter**：用于日期和时间的格式化和解析。

   ```java
   DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
   String formattedDateTime = LocalDateTime.now().format(formatter);
   LocalDateTime parsedDateTime = LocalDateTime.parse("2023-09-25 14:30:00", formatter);
   ```

8. **TemporalAdjusters**：提供了一些有用的日期调整器，例如获取某月的第一个周一。

   ```java
   LocalDate firstMondayOfSeptember = LocalDate.of(2023, 9, 1).with(TemporalAdjusters.firstInMonth(DayOfWeek.MONDAY));
   ```

## 3.3 Math

`java.lang.Math` 类包含了一些常用的数学方法，用于执行各种数学运算。以下是一些常用的 `Math` 类方法：

1. **绝对值相关方法：**
   - `abs(x)`：返回给定数的绝对值。
   - `max(x, y)`：返回两个数中较大的那个。
   - `min(x, y)`：返回两个数中较小的那个。
2. **舍入相关方法：**
   - `ceil(x)`：将参数向正无穷方向舍入为最接近的整数。
   - `floor(x)`：将参数向负无穷方向舍入为最接近的整数。
   - `round(x)`：将参数四舍五入为最接近的整数。
   - `rint(x)`：将参数四舍五入为最接近的整数，如果两个整数同样接近，则选择偶数。
3. **指数和对数相关方法：**
   - `exp(x)`：返回指数函数 e^x 的值。
   - `log(x)`：返回自然对数（以 e 为底）的值。
   - `pow(x, y)`：返回 x 的 y 次方。
   - `sqrt(x)`：返回给定数的平方根。
4. **三角函数相关方法：**
   - `sin(x)`：返回给定角度的正弦值。
   - `cos(x)`：返回给定角度的余弦值。
   - `tan(x)`：返回给定角度的正切值。
   - `asin(x)`：返回给定值的反正弦值。
   - `acos(x)`：返回给定值的反余弦值。
   - `atan(x)`：返回给定值的反正切值。
   - `toRadians(x)`：将角度从度数转换为弧度。
   - `toDegrees(x)`：将角度从弧度转换为度数。
5. **随机数生成方法：**
   - `random()`：返回一个伪随机 double 值，范围在 [0.0, 1.0) 之间。

## 3.4 System

`java.lang.System` 类是Java标准库中的一个类，它提供了一系列用于与系统交互的方法，包括访问系统属性、标准输入输出、以及进行垃圾回收等。以下是一些常见的 `System` 类方法和用法：

1. **标准输入输出（I/O）：**

   - 
     System.out
     

     标准输出流，通常用于向控制台打印信息。

     ```java
     System.out.println("Hello, world!"); // 打印文本到控制台
     ```

   - 
     System.err
     

     标准错误流，用于输出错误信息。

     ```java
     System.err.println("An error occurred!"); // 打印错误信息到控制台
     ```

   - 
     System.in
     

     标准输入流，通常用于从控制台读取用户输入。

     ```java
     Scanner scanner = new Scanner(System.in);
     System.out.print("Enter your name: ");
     String name = scanner.nextLine();
     ```

2. **系统属性：**

   - 
     System.getProperty(String key)
     

     ：获取系统属性的值，可以用于获取系统信息，如操作系统类型、Java版本等。

     ```java
     String osName = System.getProperty("os.name");
     String javaVersion = System.getProperty("java.version");
     ```

3. **垃圾回收：**

   - 
     System.gc()
     

     ：请求系统进行垃圾回收操作。注意，具体的垃圾回收时机和行为是由JVM决定的，所以不一定会立即执行垃圾回收。

     ```java
     System.gc(); // 请求进行垃圾回收
     ```

4. **程序终止：**

   - ```java
     System.exit(int status)
     ```

     终止当前Java虚拟机的运行，参数通常用于指示程序的退出状态。0 表示正常退出，非零值通常用于表示异常退出。

     ```java
     System.exit(0); // 正常退出
     ```
   
5. **时间获取：**

   - ```
     System.currentTimeMillis()
     ```

     ：返回当前时间的毫秒数，通常用于性能分析和计时。

     ```java
     long startTime = System.currentTimeMillis();
     // 执行一些代码
     long endTime = System.currentTimeMillis();
     long elapsedTime = endTime - startTime;
     ```

6. **数组拷贝：**

   - ```java
     System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
     ```

     ：用于将源数组的一部分复制到目标数组的指定位置。

     ```java
     int[] sourceArray = {1, 2, 3, 4, 5};
     int[] destArray = new int[5];
     System.arraycopy(sourceArray, 0, destArray, 0, 5);
     ```

`System` 类提供了许多有用的方法，可以用于访问系统资源、执行一些底层操作，以及进行基本的输入输出。在实际编程中，它通常用于调试、性能分析、系统属性获取等操作。但要注意，在大多数情况下，直接与系统资源交互的需求不多，因为Java提供了更高级的库和API来完成常见的任务。

## 3.5 Random

在Java中，你可以使用 `java.util.Random` 类来生成随机数。以下是使用 `Random` 类的基本方法：

1. **创建 Random 对象：**

   首先，你需要创建一个 `Random` 对象，可以通过以下方式之一来实现：

   ```java
   // 使用默认种子创建 Random 对象
   Random random = new Random();
   
   // 使用指定种子创建 Random 对象
   long seed = 123456789L; // 可以是任何长整数
   Random seededRandom = new Random(seed);
   ```

   通常情况下，如果你不需要指定特定的种子，可以使用无参数的构造函数创建 `Random` 对象，它会使用系统时间作为默认种子。

2. **生成随机整数：**

   使用 `nextInt()` 方法可以生成一个随机整数：

   ```java
   int randomNumber = random.nextInt(); // 生成任意范围的随机整数
   ```

   如果你希望生成在指定范围内的随机整数，可以使用 `nextInt(int bound)` 方法：

   ```java
   int min = 1;
   int max = 100;
   int randomInRange = random.nextInt(max - min + 1) + min; // 生成1到100之间的随机整数
   ```

3. **生成随机浮点数：**

   使用 `nextDouble()` 方法可以生成一个随机的 double 值，范围在 [0.0, 1.0) 之间：

   ```java
   double randomDouble = random.nextDouble(); // 生成0.0到1.0之间的随机浮点数
   ```

4. **生成随机布尔值：**

   使用 `nextBoolean()` 方法可以生成一个随机的布尔值（`true` 或 `false`）：

   ```java
   boolean randomBoolean = random.nextBoolean(); // 随机生成true或false
   ```

# 4 泛型

## 4.1 介绍

Java中的泛型是一种编程机制，它允许你在类、接口和方法中使用类型参数，以在不同情况下使用相同的代码来处理不同的数据类型。泛型的主要目的是提高代码的重用性、类型安全性和可读性。

使用泛型，你可以定义类、接口或方法，使其能够处理多种数据类型而不必在每次使用时进行强制类型转换。泛型类、泛型接口和泛型方法的定义都可以包含类型参数。类型参数可以在定义时指定，然后在实际使用时传入具体的类型。

以下是一个简单的泛型类的示例：

```java
public class GenericBox<T> {
    private T value;

    public GenericBox(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}
```

在这个示例中，`GenericBox` 是一个泛型类，它有一个类型参数 `T`。你可以创建 `GenericBox` 的实例，将不同类型的数据存储在其中，而无需进行显式的类型转换。

例如：

```java
GenericBox<Integer> intBox = new GenericBox<>(42);
Integer intValue = intBox.getValue(); // 不需要强制类型转换

GenericBox<String> strBox = new GenericBox<>("Hello, Generics!");
String strValue = strBox.getValue(); // 不需要强制类型转换
```

这使得代码更灵活，可以在不同的情况下使用相同的泛型类，而不必为每种数据类型创建不同的类或方法。泛型还有助于在编译时检测类型错误，提高了代码的安全性。

在Java中，尖括号 `<>` 主要用于泛型（Generics）的定义和使用。泛型是Java中的一项重要特性，允许你编写通用的、类型安全的代码，以便在运行时处理不同类型的数据。

以下是 `<>` 的用法和相关概念：

1. **泛型类 (Generic Class):** 你可以创建一个类，其中包含一个或多个类型参数，用 `<>` 括起来，然后在类的定义中使用这些类型参数。这样的类被称为泛型类。

   ```java
   public class MyGenericClass<T> {
       private T value;
   
       public MyGenericClass(T value) {
           this.value = value;
       }
   
       public T getValue() {
           return value;
       }
   }
   ```

2. **泛型接口 (Generic Interface):** 类似于泛型类，你可以创建泛型接口，使接口中的方法具有类型参数。

   ```java
   public interface MyGenericInterface<T> {
       T getDefaultValue();
   }
   ```

3. **泛型方法 (Generic Method):** 你可以在普通类或非泛型类中定义泛型方法，使用 `<>` 括起来的类型参数，以便在方法级别处理不同类型的数据。

   ```java
   public <T> T getFirstElement(List<T> list) {
       if (list.isEmpty()) {
           return null;
       }
       return list.get(0);
   }
   ```

4. **通配符 (Wildcard):** `<>` 也用于通配符的定义，通常与泛型方法和泛型类一起使用，以表示某些不确定的类型。

   - `<?>` 表示无界通配符，用于表示可以接受任何类型的数据。
   - `<? extends T>` 表示上界通配符，用于表示只能接受类型 `T` 或其子类型的数据。
   - `<? super T>` 表示下界通配符，用于表示只能接受类型 `T` 或其父类型的数据。

   例如，`List<?>` 表示一个可以包含任何类型的元素的列表。

5. **类型参数的使用:** 在使用泛型时，你可以将具体的类型传递给泛型类、泛型接口或泛型方法，以实例化它们。

   ```java
   MyGenericClass<Integer> intObject = new MyGenericClass<>(42);
   MyGenericInterface<String> stringObject = new MyGenericInterface<String>() {
       @Override
       public String getDefaultValue() {
           return "Default";
       }
   };
   ```

总之，尖括号 `<>` 在Java中用于定义和使用泛型，允许你编写更通用和类型安全的代码，以在不同类型的数据上执行操作。泛型提高了代码的重用性和可读性，同时提供了更强的类型检查。

## 4.2 collection

![image-20230926142725652](C:\Users\7878\AppData\Roaming\Typora\typora-user-images\image-20230926142725652.png)

在Java中，`Collection` 是一个接口，它表示一组对象，通常用于存储和操作多个元素。`Collection` 接口是Java集合框架的一部分，它定义了一系列用于管理和操作元素集合的通用方法。

`Collection` 接口是Java集合框架的根接口，它有许多子接口和实现类，包括`List`、`Set`、`Queue`等，每个子接口和实现类都提供了不同的数据结构和行为，以满足不同的需求。

下面是一些常用的`Collection`接口的子类：

1. **List:** `List` 接口表示有序的元素集合，允许重复元素。常见的实现类包括 `ArrayList`、`LinkedList` 和 `Vector`。你可以按索引访问元素，允许插入、删除和替换元素。
2. **Set:** `Set` 接口表示无序的元素集合，不允许重复元素。常见的实现类包括 `HashSet`、`LinkedHashSet` 和 `TreeSet`。集合中的元素不按顺序存储，而且不允许重复。
3. **Queue:** `Queue` 接口表示一个队列，通常按照先进先出（FIFO）的顺序处理元素。常见的实现类包括 `LinkedList` 和 `PriorityQueue`。它通常用于任务调度和处理等场景。

使用`Collection`接口和其子接口的步骤如下：

1. **导入必要的包：** 你需要导入`java.util`包，因为集合框架的类和接口都在这个包中。

2. **创建集合对象：** 选择适当的集合实现类，创建一个集合对象。

   ```java
   List<String> myList = new ArrayList<>(); // 创建一个ArrayList集合
   Set<Integer> mySet = new HashSet<>();   // 创建一个HashSet集合
   ```

3. **操作集合：** 使用集合对象的方法来添加、删除、查询和遍历元素。

   ```java
   // 向List中添加元素
   myList.add("Apple");
   myList.add("Banana");
   
   // 从Set中删除元素
   mySet.add(1);
   mySet.add(2);
   mySet.remove(1);
   
   // 遍历List中的元素
   for (String fruit : myList) {
       System.out.println(fruit);
   }
   ```

4. **其他操作：** 根据需要，可以使用集合的其他方法来执行搜索、排序、过滤等操作。

`Collection` 接口和其子类提供了丰富的方法来处理不同类型的集合，根据具体需求选择合适的集合类型和方法来操作数据。它们是Java中常用的数据结构，用于处理和管理多个元素的集合。

## 4.3 List

在Java中，`List` 是一个接口，表示有序的元素集合，允许重复元素。`List` 接口继承自 `Collection` 接口，并定义了一系列方法，用于操作和管理元素列表。你可以使用`List`来存储一组元素，并按照它们的插入顺序来访问、添加、删除和修改元素。

以下是使用 `List` 的基本步骤：

1. **导入必要的包：** 在使用 `List` 之前，首先需要导入 `java.util` 包，因为 `List` 接口和相关的类都在这个包中。

   ```java
   import java.util.List;
   import java.util.ArrayList; // 或其他List的实现类
   ```

2. **创建 `List` 对象：** 选择一个 `List` 接口的实现类（例如 `ArrayList`、`LinkedList` 等），创建一个 `List` 对象。

   ```java
   List<String> myList = new ArrayList<>(); // 创建一个ArrayList集合
   ```

3. **操作 `List`：** 使用 `List` 对象的方法来添加、删除、查询和遍历元素。

   ```java
   // 向List中添加元素
   myList.add("Apple");
   myList.add("Banana");
   myList.add("Cherry");
   
   // 获取List的大小
   int size = myList.size(); // 返回3，因为有3个元素
   
   // 获取指定位置的元素
   String fruit = myList.get(1); // 返回"Banana"
   
   // 修改元素
   myList.set(0, "Orange"); // 将第一个元素从"Apple"修改为"Orange"
   
   // 删除元素
   myList.remove(2); // 删除第三个元素"Cherry"
   
   // 遍历List中的元素
   for (String item : myList) {
       System.out.println(item);
   }
   ```

4. **其他操作：** 根据需要，可以使用 `List` 的其他方法来执行搜索、排序、过滤等操作。例如，你可以使用 `contains` 方法检查元素是否存在于列表中，使用 `sort` 方法对列表进行排序等。

   ```java
   // 检查元素是否存在于List中
   boolean containsBanana = myList.contains("Banana"); // 返回true
   
   // 对List进行排序
   Collections.sort(myList); // 对列表元素按照自然顺序排序
   ```

5. **注意事项：**

   - `List` 是有序的，允许元素重复。元素的顺序由插入顺序决定。
   - `List` 的索引从0开始，你可以使用索引来访问元素。
   - `List` 接口提供了丰富的方法来处理列表，包括添加、删除、修改、遍历等操作。

根据你的具体需求，选择适当的 `List` 实现类以及方法来操作元素列表。`ArrayList` 是一个常用的 `List` 实现类，通常在不需要频繁插入和删除元素的情况下使用，而 `LinkedList` 在需要频繁插入和删除元素的情况下可能更加高效。



对于一个使用迭代器（Iterator）来遍历集合的过程，初始时迭代器并不包含任何元素信息，而是通过 `.next()` 方法来获取元素的信息。这是因为迭代器是一种用于顺序访问集合中元素的对象，它的初始位置位于第一个元素之前（或集合的开头），只有调用 `.next()` 方法才会移动迭代器到下一个元素，同时返回当前元素的值。

以下是解释为什么需要使用 `.next()` 方法来获取元素信息的原因：

1. **初始位置在第一个元素之前：** 迭代器的初始位置通常是在集合的第一个元素之前（或集合的开头），这意味着在迭代器创建后，它并不指向任何元素。如果你直接尝试访问迭代器的当前元素，它将返回一个空值或抛出异常。
2. **控制迭代过程：** 使用 `.next()` 方法可以精确控制迭代过程，让你决定何时移动到下一个元素。这允许你在处理完当前元素后决定是否继续迭代或停止迭代，从而更加灵活地操作集合中的元素。
3. **提供当前元素的值：** `.next()` 方法返回迭代器当前位置的元素，并将迭代器移动到下一个位置。这样，你可以在每次调用 `.next()` 方法后获得当前元素的值，从而进行进一步的处理，比如打印、修改或使用这个元素。

```java
/**
 * 学生类
 */
public class Student {
    public String id;
    public String name;
    public Student(String id, String name){
        this.id = id;
        this.name = name;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id='" + id + '\'' +
                ", name='" + name + '\'' +
                '}';
    }
}

import java.util.*;


public class ListTest {

    //集合后面的<>代表泛型的意思
    //泛型是规定了集合元素的类型
    /**
     * 用于存放学生的List
     */
    public List<Student> students;


    public ListTest() {
        this.students = new ArrayList<Student>();
    }

    /**
     * 用于往students中添加学生
     */
    public void testAdd() {
        // 创建一个学生对象，并通过调用add方法，添加到学生管理List中
        Student st1 = new Student("1", "张三");
        students.add(st1);

        // 取出 List中的Student对象 索引为0 也就是第一个
        Student temp = students.get(0);
        System.out.println("添加了学生：" + temp.id + ":" + temp.name);

        Student st2 = new Student("2", "李四");
        //添加到list中，插入到索引为0的位置，也就是第一个
        students.add(0, st2);
        Student temp2 = students.get(0);
        System.out.println("添加了学生：" + temp2.id + ":" + temp2.name);

        // 对象数组的形式添加
        Student[] student = {new Student("3", "王五"), new Student("4", "马六")};

        // Arrays类包含用来操作数组（比如排序和搜索）的各种方法，asList() 方法用来返回一个受指定数组支持的固定大小的列表
        students.addAll(Arrays.asList(student));
        Student temp3 = students.get(2);
        Student temp4 = students.get(3);
        System.out.println("添加了学生：" + temp3.id + ":" + temp3.name);
        System.out.println("添加了学生：" + temp4.id + ":" + temp4.name);
        Student[] student2 = {new Student("5", "周七"), new Student("6", "赵八")};
        students.addAll(2, Arrays.asList(student2));
        Student temp5 = students.get(2);
        Student temp6 = students.get(3);
        System.out.println("添加了学生：" + temp5.id + ":" + temp5.name);
        System.out.println("添加了学生：" + temp6.id + ":" + temp6.name);
    }


    /**
     * 取得List中的元素的方法
     */
    public void testGet() {
        int size = students.size();
        for (int i = 0; i < size; i++) {
            Student st = students.get(i);
            System.out.println("学生：" + st.id + ":" + st.name);

        }
    }


    /**
     * 通过迭代器来遍历
     * 迭代器的工作是遍历并选择序列中的对象，Java 中 Iterator 只能单向移动
     */
    public void testIterator() {
        // 通过集合的iterator方法，取得迭代器实例
        Iterator<Student> it = students.iterator();
        System.out.println("有如下学生（通过迭代器访问）：");
        while (it.hasNext()) {

            Student st = it.next();
            System.out.println("学生" + st.id + ":" + st.name);
        }
    }

    /**
     * 通过for each 方法访问集合元素
     *
     */
    public void testForEach() {
        System.out.println("有如下学生（通过for each）：");
        for (Student obj : students) {
            Student st = obj;
            System.out.println("学生：" + st.id + ":" + st.name);
        }
        //使用java8 Steam将学生排序后输出
        students.stream()//创建Stream
                //通过学生id排序
                .sorted(Comparator.comparing(x -> x.id))
                //输出
                .forEach(System.out::println);
    }

    /**
     * 修改List中的元素
     *
     */
    public void testModify() {
        students.set(4, new Student("3", "吴酒"));
    }

    /**
     * 删除List中的元素
     *
     */
    public void testRemove() {
        Student st = students.get(4);
        System.out.println("我是学生：" + st.id + ":" + st.name + "，我即将被删除");
        students.remove(st);
        System.out.println("成功删除学生！");
        testForEach();
    }


    public static void main(String[] args) {
        ListTest lt = new ListTest();
        lt.testAdd();
        lt.testGet();
        lt.testIterator();
        lt.testModify();
        lt.testForEach();
        lt.testRemove();

    }
}
```

> `ArrayList` 和 `Vector` 都是 Java 集合框架中的实现了 `List` 接口的类，它们都用于存储有序的元素集合，允许元素重复，且按照插入顺序进行存储。然而，它们之间存在一些关键区别：
>
> 1. **线程安全性：**
>    - `ArrayList` 是非线程安全的：`ArrayList` 不是线程安全的，这意味着在多线程环境中使用 `ArrayList` 时，需要额外的同步措施，否则可能会导致不确定的行为或数据损坏。
>    - `Vector` 是线程安全的：`Vector` 在每个方法上都添加了同步关键字，因此可以在多线程环境中安全使用。然而，这也可能导致在高度并发的情况下性能略有下降。
> 2. **性能：**
>    - `ArrayList` 通常比 `Vector` 更快：由于 `Vector` 实现了线程同步，因此在单线程环境下，`ArrayList` 通常比 `Vector` 更快，因为它不需要额外的同步开销。
>    - `Vector` 在多线程环境中可能更适用：如果你需要在多线程环境中使用一个线程安全的动态数组，`Vector` 可能更适合，尽管性能方面可能会略有牺牲。
> 3. **增长策略：**
>    - `ArrayList` 的增长策略是增加一半的容量：当 `ArrayList` 的容量不足以容纳新元素时，它会自动增加其容量，通常是当前容量的一半。这可以减少内存浪费。
>    - `Vector` 的增长策略是增加一倍的容量：当 `Vector` 的容量不足时，它会将容量翻倍。这可能导致更多的内存浪费，尤其在容量较大时。
> 4. **遗留特性：**
>    - `Vector` 是一个古老的类：`Vector` 是在Java早期引入的，因此它具有一些遗留的特性，如不支持泛型。相比之下，`ArrayList` 是在Java 1.2引入的，并支持泛型。
>
> 总结：一般情况下，如果你在单线程环境中使用动态数组，`ArrayList` 是一个更好的选择，因为它具有较好的性能。如果你需要在线程安全的多线程环境中使用动态数组，可以考虑使用 `Vector`。然而，现代 Java 更倾向于使用 `ArrayList`，并使用 `Collections.synchronizedList` 方法来将其转换为线程安全的形式，以获得更好的性能。

## 4.4 Map

在 Java 中，`Map` 是一种非常有用的数据结构，用于存储键值对（key-value pairs）。每个键都唯一，而与每个键关联的值可以重复。`Map` 提供了一种快速查找和检索值的方式，通常用于表示和管理数据的关联关系。

以下是 Java 中使用 `Map` 的基本操作和示例：

1. 创建一个 Map 对象：

你可以使用 `HashMap`、`TreeMap`、`LinkedHashMap` 等 `Map` 的实现类来创建一个 `Map` 对象。例如：

```java
import java.util.*;

Map<String, Integer> map = new HashMap<>(); // 创建一个 HashMap，键的类型是 String，值的类型是 Integer
```

2. 添加键值对：

使用 `put` 方法将键值对添加到 `Map` 中：

```java
map.put("Alice", 25);
map.put("Bob", 30);
map.put("Charlie", 28);
```

3. 获取值：

使用 `get` 方法根据键获取对应的值：

```java
int age = map.get("Alice"); // 获取键为 "Alice" 的值，age 等于 25
```

4. 检查键是否存在：

使用 `containsKey` 方法来检查某个键是否存在于 `Map` 中：

```java
boolean containsAlice = map.containsKey("Alice"); // containsAlice 等于 true
boolean containsDavid = map.containsKey("David"); // containsDavid 等于 false
```

5. 遍历 Map：

你可以使用不同的方式来遍历 `Map`，例如使用 `keySet()`、`values()` 或 `entrySet()` 方法。以下是使用 `entrySet()` 的示例：

```java
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    String key = entry.getKey();
    int value = entry.getValue();
    System.out.println(key + " -> " + value);
}
```

6. 删除键值对：

使用 `remove` 方法来删除指定键的键值对：

```java
map.remove("Bob"); // 删除键为 "Bob" 的键值对
```

7. 获取 Map 的大小：

使用 `size` 方法获取 `Map` 中键值对的数量：

```java
int size = map.size(); // 获取 Map 中键值对的数量
```

这些是 `Map` 基本操作的示例。`Map` 提供了强大的功能，可以用于解决各种数据关联问题，如字典、缓存、计数器等。你可以根据具体的需求选择合适的 `Map` 实现类以及操作方法。

```java
public class Course {
    public String id;
    public String name;
    public Course(String id, String name){
        this.id = id;
        this.name = name;
    }
}
```

```java
// MapTest.java
import java.util.HashMap;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Scanner;
import java.util.Set;

public class MapTest {

    /**
     * 用来承装课程类型对象
     */
    public Map<String, Course> courses;

    /**
     * 在构造器中初始化 courses 属性
     * @param args
     */
    public MapTest() {
        this.courses = new HashMap<String, Course>();
    }

    /**
     * 测试添加：输入课程 ID，判断是否被占用
     * 若未被占用，输入课程名称，创建新课程对象
     * 并且添加到 courses 中
     * @param args
     */
    public void testPut() {
        //创建一个 Scanner 对象，用来获取输入的课程 ID 和名称
        Scanner console = new Scanner(System.in);

        for(int i = 0; i < 3; i++) {
            System.out.println("请输入课程 ID：");
            String ID = console.next();
            //判断该 ID 是否被占用
            Course cr = courses.get(ID);
            if(cr == null){
                //提示输入课程名称
                System.out.println("请输入课程名称：");
                String name = console.next();
                //创建新的课程对象
                Course newCourse = new Course(ID,name);
                //通过调用 courses 的 put 方法，添加 ID-课程映射
                courses.put(ID, newCourse);
                System.out.println("成功添加课程：" + courses.get(ID).name);
            }
            else {
                System.out.println("该课程 ID 已被占用");
                continue;
            }
        }
    }

    /**
     * 测试 Map 的 keySet 方法
     * @param args
     */

    public void testKeySet() {
        //通过 keySet 方法，返回 Map 中的所有键的 Set 集合
        Set<String> keySet = courses.keySet();
        //遍历 keySet，取得每一个键，在调用 get 方法取得每个键对应的 value
        for(String crID: keySet) {
            Course cr = courses.get(crID);
            if(cr != null){
                System.out.println("课程：" + cr.name);
            }
        }
    }

    /**
     * 测试删除 Map 中的映射
     * @param args
     */
    public void testRemove() {
        //获取从键盘输入的待删除课程 ID 字符串
        Scanner console = new Scanner(System.in);
        while(true){
            //提示输出待删除的课程 ID
            System.out.println("请输入要删除的课程 ID！");
            String ID = console.next();
            //判断该 ID 是否对应的课程对象
            Course cr = courses.get(ID);
            if(cr == null) {
                //提示输入的 ID 并不存在
                System.out.println("该 ID 不存在！");
                continue;
            }
            courses.remove(ID);
            System.out.println("成功删除课程" + cr.name);
            break;
        }
    }

    /**
     * 通过 entrySet 方法来遍历 Map
     * @param args
     */
    public void testEntrySet() {
        //通过 entrySet 方法，返回 Map 中的所有键值对
        Set<Entry<String,Course>> entrySet = courses.entrySet();
        for(Entry<String,Course> entry: entrySet) {
            System.out.println("取得键：" + entry.getKey());
            System.out.println("对应的值为：" + entry.getValue().name);
        }
    }

    /**
     * 利用 put 方法修改Map 中的已有映射
     * @param args
     */
    public void testModify(){
        //提示输入要修改的课程 ID
        System.out.println("请输入要修改的课程 ID：");
        //创建一个 Scanner 对象，去获取从键盘上输入的课程 ID 字符串
        Scanner console = new Scanner(System.in);
        while(true) {
            //取得从键盘输入的课程 ID
            String crID = console.next();
            //从 courses 中查找该课程 ID 对应的对象
            Course course = courses.get(crID);
            if(course == null) {
                System.out.println("该 ID 不存在！请重新输入！");
                continue;
            }
            //提示当前对应的课程对象的名称
            System.out.println("当前该课程 ID，所对应的课程为：" + course.name);
            //提示输入新的课程名称，来修改已有的映射
            System.out.println("请输入新的课程名称：");
            String name = console.next();
            Course newCourse = new Course(crID,name);
            courses.put(crID, newCourse);
            System.out.println("修改成功！");
            break;
        }
    }

    public static void main(String[] args) {
        MapTest mt = new MapTest();
        mt.testPut();
        mt.testKeySet();
        mt.testRemove();
        mt.testModify();
        mt.testEntrySet();

    }
}
```

## 4.5 Collection

`java.util.Collections` 类提供了许多实用的静态方法，用于对集合进行操作。以下是一些常见的用法示例：

1. **排序列表**：

   ```java
   List<Integer> numbers = new ArrayList<>();
   numbers.add(3);
   numbers.add(1);
   numbers.add(2);
   Collections.sort(numbers); // 对列表进行排序
   ```

2. **反转列表**：

   ```java
   List<String> names = new ArrayList<>();
   names.add("Alice");
   names.add("Bob");
   names.add("Charlie");
   Collections.reverse(names); // 反转列表中的元素顺序
   ```

3. **查找元素**：

   ```java
   List<Integer> numbers = new ArrayList<>();
   numbers.add(1);
   numbers.add(2);
   numbers.add(3);
   int index = Collections.binarySearch(numbers, 2); // 在有序列表中执行二分查找
   ```

4. **随机打乱列表**：

   ```java
   List<String> cards = new ArrayList<>();
   cards.add("Ace");
   cards.add("King");
   cards.add("Queen");
   Collections.shuffle(cards); // 随机打乱列表中的元素顺序
   ```

5. **复制列表**：

   ```java
   List<String> source = new ArrayList<>();
   source.add("A");
   source.add("B");
   List<String> destination = new ArrayList<>();
   Collections.copy(destination, source); // 将一个列表的元素复制到另一个列表中
   ```

6. **填充列表**：

   ```java
   List<Integer> numbers = new ArrayList<>(Collections.nCopies(5, 0)); // 使用指定元素填充列表
   ```

7. **创建不可修改的集合**：

   ```java
   List<String> immutableList = Collections.unmodifiableList(originalList); // 创建不可修改的列表
   ```

# 5 异常

## 5.1 分类

在Java中，异常分为三大类：

1. **受检异常（Checked Exceptions）**：

   - 受检异常是指在编译时必须处理的异常。这些异常通常是由外部因素引起的，比如文件不存在、网络连接问题等。如果一个方法可能会抛出受检异常，要么在方法内部使用`try-catch`块捕获异常，要么在方法签名中使用`throws`关键字声明该异常，通知调用者处理异常。

   ```java
   try {
       // 可能抛出受检异常的代码
   } catch (IOException e) {
       // 处理受检异常
   }
   ```

2. **未受检异常（Unchecked Exceptions，也称为运行时异常）**：`RuntimeException`

   - 未受检异常是指在运行时可能会发生的异常，通常由程序错误引起，比如空指针异常（`NullPointerException`）、数组越界异常（`ArrayIndexOutOfBoundsException`）等。这些异常是`RuntimeException`类及其子类的实例。在编程中，通常不需要显式地捕获这些异常，但最好是在代码中预防它们的发生。

   ```java
   // 未受检异常的示例：空指针异常
   String str = null;
   int length = str.length(); // 这里会抛出空指针异常
   ```

3. **错误（Errors）**：

   - 错误是指虚拟机无法处理的严重问题，通常由系统故障引起，比如内存溢出错误（`OutOfMemoryError`）或虚拟机崩溃。与异常不同，错误通常是不可恢复的。在编写应用程序时，我们不需要关心错误，因为它们通常是由虚拟机或底层系统引起的问题。

   ```java
   // 错误的示例：内存溢出错误
   public void recursiveMethod() {
       recursiveMethod();
   }
   ```

## 5.2 处理

在Java中，你可以使用`throws`关键字来声明和抛出异常。异常的声明和抛出通常在方法的签名部分进行。以下是如何声明和抛出异常的一般步骤：

1. **在方法签名中声明异常**：

   - 在方法的参数列表之后，使用 `throws` 关键字声明可能会被抛出的异常。可以声明多个异常，用逗号分隔。

   ```java
   public void someMethod() throws SomeException, AnotherException {
       // 方法实现
   }
   ```

2. **抛出异常**：

   - 在方法内部，如果满足某个条件导致异常情况，可以使用 `throw` 关键字抛出异常对象。

   ```java
   public void someMethod() throws SomeException {
       if (/* 满足某个条件 */) {
           throw new SomeException("发生了某种异常");
       }
       // 方法继续执行
   }
   ```

3. **捕获异常**：

   - 当调用抛出异常的方法时，你必须使用 `try-catch` 块捕获异常，或者将异常继续向上抛出（再次声明）。

   ```java
   try {
       someMethod();
   } catch (SomeException e) {
       // 处理 SomeException 异常
   } catch (AnotherException e) {
       // 处理 AnotherException 异常
   }
   ```

4. **继续抛出异常**：

   - 如果你不打算在当前方法中处理异常，而是希望将异常传递给调用者，可以在方法中继续使用 `throws` 关键字声明异常。

   ```java
   public void someMethod() throws SomeException {
       if (/* 满足某个条件 */) {
           throw new SomeException("发生了某种异常");
       }
       // 方法继续执行
   }
   ```

通过这种方式，你可以在程序中声明和抛出异常，并根据需要进行适当的异常处理或传递。

## 5.3 多异常处理

在Java中，你可以使用多个 `catch` 块来捕获多种异常。每个 `catch` 块用于捕获特定类型的异常，并提供相应的处理逻辑。下面是捕获多个异常的基本语法：

```java
try {
    // 一些可能抛出异常的代码
} catch (ExceptionType1 e1) {
    // 处理 ExceptionType1 类型的异常
} catch (ExceptionType2 e2) {
    // 处理 ExceptionType2 类型的异常
} catch (ExceptionType3 e3) {
    // 处理 ExceptionType3 类型的异常
} // and so on for more catch blocks
```

- 在 `try` 块中，你编写可能抛出异常的代码。
- 对于每种可能抛出的异常类型，你可以使用一个 `catch` 块来捕获和处理该类型的异常。
- 按照需要，你可以定义多个 `catch` 块，每个 `catch` 块捕获不同类型的异常，并提供相应的处理逻辑。

如果某个异常类型是另一个异常类型的子类，它应该在其父类之后捕获，因为Java编译器会按照从子类到父类的顺序进行匹配。

## 5.4 自定义异常

在Java中，你可以通过创建一个继承自`Exception`或`RuntimeException`的类来自定义异常。这个自定义异常类应该提供自定义异常的特定行为和信息。

以下是创建自定义异常的基本步骤：

创建自定义异常类

- 创建一个继承自 `Exception`（受检异常）或 `RuntimeException`（未受检异常）的类。

```java
// 自定义受检异常类
public class CustomCheckedException extends Exception {
    public CustomCheckedException(String message) {
        super(message);
    }
}

// 自定义未受检异常类
public class CustomUncheckedException extends RuntimeException {
    public CustomUncheckedException(String message) {
        super(message);
    }
}
```

**添加构造函数**：

- 在自定义异常类中，添加构造函数以接受异常消息并调用父类的构造函数。

**使用自定义异常**：

- 在需要抛出自定义异常的代码中，创建自定义异常的对象并抛出。

```java
public class Example {
    public void someMethod() throws CustomCheckedException {
        // 某些情况下抛出自定义受检异常
        throw new CustomCheckedException("这是自定义受检异常");
    }

    public void anotherMethod() {
        // 某些情况下抛出自定义未受检异常
        throw new CustomUncheckedException("这是自定义未受检异常");
    }
}
```

捕获自定义异常

- 在调用抛出自定义异常的方法时，你可以使用 `try-catch` 块捕获自定义异常并处理它。

```java
try {
    Example example = new Example();
    example.someMethod();
} catch (CustomCheckedException e) {
    // 处理自定义受检异常
    e.printStackTrace();
}
```

## 5.5 异常堆栈

异常堆栈（也称为堆栈跟踪或调用堆栈）是在程序执行过程中发生异常时记录的一组调用方法的信息。它提供了一个关于异常发生位置和异常传播路径的详细视图。异常堆栈通常包括以下信息：

1. 方法调用顺序：异常堆栈列出了程序中从发生异常的地方开始到异常被捕获或程序终止的方法调用序列。这些方法调用以栈的形式排列，最上面的是最近调用的方法，最下面的是最初的调用。
2. 类名和方法名：堆栈中的每个元素都包括了引发异常的方法的类名和方法名。这有助于确定异常发生的确切位置。
3. 行号信息：通常，异常堆栈还包括了引发异常的方法中出现异常的代码行号。这使得程序员能够准确定位问题代码的位置。

异常堆栈对于调试和诊断问题非常有用。当程序抛出异常时，异常堆栈可以帮助开发人员追踪异常的来源，找出问题的根本原因，并更轻松地修复代码中的错误。堆栈跟踪也可以用于记录异常，以便后续的故障排除或错误报告。

```java
public class ExceptionStackTrace {
    private static void method1() {
        method2();
    }

    private static void method2() {
        throw new NullPointerException();
    }
    public static void main(String[] args) {
        try {
            method1();
        } catch (Exception e) {
            //打印堆栈轨迹
            e.printStackTrace();
        }
    }
}
```

```java
java.lang.NullPointerException
    at ExceptionStackTrace.method2(ExceptionStackTrace.java:7)
    at ExceptionStackTrace.method1(ExceptionStackTrace.java:3)
    at ExceptionStackTrace.main(ExceptionStackTrace.java:11)
```

# 6 Lambda

## 6.1 使用

Lambda表达式是Java 8引入的一种函数式编程特性，用于简化匿名内部类的编写以及在函数式接口中定义行为。要实现Lambda表达式，你需要按照以下基本语法规则进行操作：

1. **确定函数式接口**：首先，你需要有一个函数式接口，它只包含一个抽象方法。函数式接口是一个具有单个抽象方法的接口。
2. **定义Lambda表达式**：Lambda表达式的一般形式是 `(参数) -> 表达式`。参数是方法的参数，表达式是方法的实现。可以使用箭头符号 `->` 分隔参数和表达式。
3. **调用Lambda表达式**：将Lambda表达式分配给一个接口类型的变量，然后可以使用该变量来调用Lambda表达式。

下面是一个简单示例，展示如何创建和使用Lambda表达式：

```java
// 步骤 1：确定函数式接口
@FunctionalInterface
interface MyFunction {
    int apply(int a, int b);
}

public class LambdaExample {
    public static void main(String[] args) {
        // 步骤 2：定义Lambda表达式
        MyFunction addition = (a, b) -> a + b;
        MyFunction subtraction = (a, b) -> a - b;

        // 步骤 3：调用Lambda表达式
        int result1 = addition.apply(5, 3); // 调用Lambda表达式执行加法
        int result2 = subtraction.apply(5, 3); // 调用Lambda表达式执行减法

        System.out.println("Addition result: " + result1);
        System.out.println("Subtraction result: " + result2);
    }
}
```

在这个示例中，我们首先定义了一个函数式接口 `MyFunction`，它具有一个抽象方法 `apply`。然后，我们创建了两个Lambda表达式 `addition` 和 `subtraction`，并使用它们执行加法和减法操作。

Lambda表达式的强大之处在于可以将它们传递给方法、将它们作为参数传递给其他方法，并以一种简洁的方式表达行为。这在处理集合、多线程等场景中非常有用。

## 6.2 作用域

Lambda表达式的作用域是指Lambda表达式可以访问哪些变量以及它们的生命周期。Lambda表达式的作用域是根据以下规则确定的：

1. **局部变量**：Lambda表达式可以访问外部方法中的局部变量，但这些局部变量必须满足以下条件：
   - 局部变量必须是隐式或显式地声明为 `final` 或 `effectively final`。这意味着一旦赋值后，不能再修改这些变量的值。从Java 8开始，如果变量在赋值后没有被再次赋值，它被认为是"effectively final"。
   - 如果Lambda表达式在一个线程中使用了某个局部变量，那么这个变量必须是线程安全的。
2. **成员变量和静态变量**：Lambda表达式可以自由访问包含它的类的成员变量和静态变量，就像普通的类方法一样。
3. **方法参数**：Lambda表达式可以访问外部方法的参数，但参数也必须是 `final` 或 `effectively final`。

下面是一个示例，演示了Lambda表达式的作用域：

```java
public class LambdaScopeExample {
    private int instanceVar = 10;
    private static int staticVar = 20;

    public void lambdaInMethod() {
        int localVar = 30; // 局部变量

        // Lambda 表达式可以访问局部变量 localVar 和 instanceVar，以及静态变量 staticVar
        MyFunctionalInterface myLambda = () -> {
            System.out.println("instanceVar: " + instanceVar);
            System.out.println("staticVar: " + staticVar);
            System.out.println("localVar: " + localVar);
        };

        myLambda.doSomething();
    }

    public static void main(String[] args) {
        LambdaScopeExample example = new LambdaScopeExample();
        example.lambdaInMethod();
    }

    @FunctionalInterface
    interface MyFunctionalInterface {
        void doSomething();
    }
}
```

在这个示例中，Lambda表达式 `myLambda` 可以访问 `instanceVar`（成员变量）、`staticVar`（静态变量），以及 `localVar`（局部变量），因为它们都符合Lambda表达式的作用域规则。如果你尝试在Lambda表达式内部修改 `localVar` 的值，将会导致编译错误，因为它不是`final`或`effectively final`的。

> 相对于普通的类方法，Lambda表达式的主要区别在于它们可以访问外部作用域的变量，这是通过闭包实现的。以下是Lambda表达式与普通类方法之间的主要区别：
>
> 1. **变量访问**：
>    - **Lambda表达式**：Lambda表达式可以访问包含它们的方法的局部变量（必须是`final`或`effectively final`），成员变量，以及静态变量。
>    - **普通类方法**：普通类方法只能访问它们所属类的成员变量和静态变量，不能直接访问方法中的局部变量。
> 2. **this关键字**：
>    - **Lambda表达式**：Lambda表达式中的`this`关键字指向它所在的外部类。
>    - **普通类方法**：普通类方法中的`this`关键字指向该类的实例。
> 3. **对接口的依赖**：
>    - **Lambda表达式**：Lambda表达式依赖于函数式接口，即接口中只有一个抽象方法。它们可以实现该接口并提供方法实现。
>    - **普通类方法**：普通类方法可以属于任何类，无需依赖于特定的接口。
> 4. **简洁性**：
>    - **Lambda表达式**：Lambda表达式通常比传统的匿名内部类更为简洁，可以在更少的代码行中表达相同的逻辑。
> 5. **使用场景**：
>    - **Lambda表达式**：适用于简单的功能接口实现，尤其是在集合处理、线程处理等函数式编程场景中。
>    - **普通类方法**：适用于一般的方法实现，可能需要较多的代码和复杂的逻辑。
>
> 总的来说，Lambda表达式提供了一种更简洁、更函数式的方法来实现特定的功能接口，特别适用于对集合进行操作或实现简单功能的情况。它们使得代码更为紧凑，更容易理解和维护。然而，在某些情况下，传统的类方法可能更适合复杂的业务逻辑或需要多个方法的情况。

## 6.3 方法引用

在Java中，方法引用是一种简化Lambda表达式的语法，用于调用已经存在的方法。它可以替代Lambda表达式，使代码更加简洁易读。

方法引用通常用于函数式接口的实例化，函数式接口是只包含一个抽象方法的接口。方法引用可以用来引用以下类型的方法：

1. 静态方法引用：引用静态方法。
2. 对象方法引用：引用特定对象的实例方法。
3. 类型方法引用：引用特定类型的任意对象的实例方法。

以下是一些方法引用的示例：

- 静态方法引用：

  ```java
  // 使用方法引用调用静态方法
  Function<Integer, Integer> square = Math::square;
  ```

- 对象方法引用：

  ```java
  // 使用方法引用调用实例方法
  List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
  names.forEach(System.out::println);
  ```

- 类型方法引用：

  ```java
  // 使用方法引用调用类型方法
  Comparator<String> stringComparator = String::compareToIgnoreCase;
  ```

方法引用通过`::`符号后跟方法名来引用方法，而不需要提供方法的具体实现，编译器会根据上下文自动推断。

## 6.4 函数式编程

`java.util.Function` 是一个函数式接口，它接受一个输入参数并返回一个结果。它定义了一个名为 `apply` 的抽象方法，用于将输入转换为输出。

该接口通常用于将操作作为参数传递给其他方法，例如在 Stream API 中进行数据处理，或者在函数式编程中进行函数组合。

以下是一个简单的示例，演示了如何使用 `java.util.Function` 接口：

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        // 创建一个 Function，将输入值乘以2并返回
        Function<Integer, Integer> multiplyBy2 = x -> x * 2;

        // 使用 apply 方法应用函数
        int result = multiplyBy2.apply(5); // 结果为 10
        System.out.println(result);
    }
}
```

在这个例子中，我们首先创建了一个 `Function` 对象 `multiplyBy2`，它将输入值乘以2。然后，我们调用 `apply` 方法将输入值 `5` 应用到函数上，得到了结果 `10`。

1. **Consumer (消费者)：**
   - **描述：** 表示接受单个输入参数并且不返回结果的操作。
   - **接口方法：** `void accept(T t)`
2. **Function (函数)：**
   - **描述：** 表示接受一个输入参数并产生一个结果的函数。
   - **接口方法：** `R apply(T t)`
3. **Supplier (供应商)：**
   - **描述：** 表示一个供应商，不接受任何参数，但返回一个结果。
   - **接口方法：** `T get()`
4. **Predicate (断言)：**
   - **描述：** 表示一个断言（布尔值函数），接受一个参数并返回一个布尔值结果。
   - **接口方法：** `boolean test(T t)`
5. **UnaryOperator (一元操作符)：**
   - **描述：** 表示一个一元操作符，接受一个参数并返回与该参数相同类型的结果。
   - **接口方法：** `T apply(T t)`
6. **BinaryOperator (二元操作符)：**
   - **描述：** 表示一个二元操作符，接受两个参数并返回与参数相同类型的结果。
   - **接口方法：** `T apply(T t1, T t2)`

```java
import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;

public class FunctionTest {
   public static void main(String args[]){
      // 创建一个包含整数的列表
      List<Integer> list = Arrays.asList(0, 1, 2, 3, 4, 5, 6, 7, 8, 9);

      System.out.println("All of the numbers:");

      // 使用 Predicate 过滤并打印所有数字
      eval(list, n->true);

      System.out.println("Even numbers:");
      // 使用 Predicate 过滤并打印偶数
      eval(list, n-> n%2 == 0 );

      System.out.println("Numbers that are greater than 5:");
      // 使用 Predicate 过滤并打印大于5的数字
      eval(list, n -> n > 5 );
   }

   // 通用的方法，接受列表和 Predicate，用于过滤和打印符合条件的元素
   public static void eval(List<Integer> list, Predicate<Integer> predicate) {
      for(Integer n: list) {
         // 使用 Predicate 测试元素是否满足条件，然后打印符合条件的元素
         if(predicate.test(n)) {
            System.out.println(n);
         }
      }
   }
}

```

# 7 Stream

## 7.1 创建流

要创建一个流（Stream）对象，你可以使用以下方式：

1. 从集合创建流：你可以从集合（如List、Set、Map等）创建一个流。Java中的集合提供了`stream()`方法来生成流。

```java
List<String> myList = Arrays.asList("apple", "banana", "cherry");
Stream<String> stream = myList.stream();
```

1. 从数组创建流：你也可以从数组创建流，使用`Arrays.stream()`方法。

```java
int[] numbers = {1, 2, 3, 4, 5};
IntStream stream = Arrays.stream(numbers);
```

1. 使用Stream.of()创建流：你可以使用`Stream.of()`方法创建一个包含指定元素的流。

```java
Stream<String> stream = Stream.of("apple", "banana", "cherry");
```

1. 使用Stream.generate()创建无限流：如果需要创建一个无限流，可以使用`Stream.generate()`方法，并传入一个生成元素的Supplier。

```java
Stream<Integer> infiniteStream = Stream.generate(() -> 1);
```

1. 使用Stream.iterate()创建无限流：类似于`Stream.generate()`，你也可以使用`Stream.iterate()`创建一个无限流，但需要提供一个初始值和一个UnaryOperator来生成后续的值。

```java
Stream<Integer> infiniteStream = Stream.iterate(1, n -> n + 1);
```

## 7.2 操作流

当使用Java中的`Stream`时，你可以执行各种操作，包括中间操作和终端操作。以下是一些`Stream`的常见用法，以及相应的示例：

**1. 过滤（Filter）：** 使用`filter`中间操作来筛选出满足条件的元素。

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
List<Integer> evenNumbers = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());
// evenNumbers 现在包含 [2, 4, 6, 8, 10]
```

**2. 映射（Map）：** 使用`map`中间操作将元素映射成新的值。

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
List<Integer> nameLengths = names.stream()
    .map(String::length)
    .collect(Collectors.toList());
// nameLengths 现在包含 [5, 3, 7]
```

**3. 排序（Sort）：** 使用`sorted`中间操作对元素进行排序。

```java
List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 9);
List<Integer> sortedNumbers = numbers.stream()
    .sorted()
    .collect(Collectors.toList());
// sortedNumbers 现在包含 [1, 2, 5, 8, 9]
```

**4. 聚合（Reduce）：** 使用`reduce`终端操作对元素进行聚合操作，如求和、求最大值、求最小值等。

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.stream()
    .reduce(0, (a, b) -> a + b);
// sum 现在等于 15
```

**5. 收集（Collect）：** 使用`collect`终端操作将流中的元素收集到一个集合中。

```java
List<String> fruits = Arrays.asList("apple", "banana", "cherry");
Set<String> fruitSet = fruits.stream()
    .collect(Collectors.toSet());
// fruitSet 现在包含 {"apple", "banana", "cherry"}
```

**6. 遍历（ForEach）：** 使用`forEach`终端操作对流中的每个元素执行指定操作。

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.stream()
    .forEach(System.out::println);
// 将每个数字打印到控制台
```

在Java中，`peek()` 方法是Java流（Stream）类提供的一个中间操作方法之一。它允许你在流的每个元素被处理时执行一个操作，但不会改变流的内容，而是返回原始流。`peek()` 方法通常用于调试和观察流的操作，以便查看流的中间状态，而不会影响流的最终结果。

该方法的签名如下：

```java
Stream<T> peek(Consumer<? super T> action)
```

其中，`action` 是一个接受类型为 `T` 的元素的消费者函数，你可以在这个函数中执行任何你想要的操作。

例如，假设你有一个整数流，你可以使用 `peek()` 方法来打印每个元素，并查看它们的值，而不改变流的内容：

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

numbers.stream()
       .peek(num -> System.out.println("Processing: " + num))
       .map(num -> num * 2)
       .forEach(System.out::println);
```

在上面的示例中，`peek()` 方法用于输出每个元素的处理状态，但不会更改流的元素。然后，`map()` 方法将每个元素乘以2，最后使用 `forEach()` 方法打印结果。这个操作链允许你在流的处理过程中观察元素的中间状态。

## 7.3 Collectors

`Collectors` 是 Java 中用于收集（或汇总）流中元素的工具类，它提供了各种用于收集数据的静态方法。`Collectors` 的主要用法包括：

**1. 收集到List、Set或其他集合类型：**

- `Collectors.toList()`：将流中的元素收集到一个`List`中。
- `Collectors.toSet()`：将流中的元素收集到一个`Set`中。
- `Collectors.toCollection(collectionFactory)`：将流中的元素收集到指定类型的集合中。

示例：

```java
List<String> names = Stream.of("Alice", "Bob", "Charlie")
    .collect(Collectors.toList());
```

**2. 收集到Map：**

- `Collectors.toMap(keyMapper, valueMapper)`：将流中的元素收集到一个`Map`中，可以指定如何映射键和值。
- `Collectors.toConcurrentMap(keyMapper, valueMapper)`：类似于`toMap`，但返回的是一个并发安全的`ConcurrentMap`。

示例：

```java
Map<String, Integer> nameLengthMap = Stream.of("Alice", "Bob", "Charlie")
    .collect(Collectors.toMap(name -> name, String::length));
```

**3. 字符串连接：**

- `Collectors.joining(delimiter)`：将流中的元素连接成一个字符串，可以指定连接符。

示例：

```java
String joinedNames = Stream.of("Alice", "Bob", "Charlie")
    .collect(Collectors.joining(", "));
// joinedNames 现在等于 "Alice, Bob, Charlie"
```

**4. 统计汇总信息：**

- `Collectors.summarizingInt(ToIntFunction)`：对`int`类型的元素进行汇总，包括计数、总和、最大值、最小值、平均值等信息。
- `Collectors.summarizingDouble(ToDoubleFunction)`：类似于`summarizingInt`，但适用于`double`类型的元素。

示例：

```java
IntSummaryStatistics stats = Stream.of(1, 2, 3, 4, 5)
    .collect(Collectors.summarizingInt(Integer::intValue));
```

**5. 分组和分区：**

- `Collectors.groupingBy(classifier)`：根据指定条件对元素进行分组，返回一个`Map`，键是分组条件，值是分组的元素列表。
- `Collectors.partitioningBy(predicate)`：根据指定条件将元素分成两组（true和false），返回一个`Map`，键是true或false，值是符合条件的元素列表。

示例：

```java
Map<Integer, List<String>> groupByLength = Stream.of("Alice", "Bob", "Charlie")
    .collect(Collectors.groupingBy(String::length));
Map<Boolean, List<String>> partitionByLength = Stream.of("Alice", "Bob", "Charlie")
    .collect(Collectors.partitioningBy(name -> name.length() > 4));
```

## 7.4 flatMap

你可以使用Java中的Stream API中的`flatMap`方法来操作流并实现合并和转换的功能。下面是使用`flatMap`的一些常见示例和用法：

**示例1：合并多个流**

假设你有多个字符串流，想将它们合并成一个单一的字符串流：

```java
Stream<String> stream1 = Stream.of("Hello", "World");
Stream<String> stream2 = Stream.of("Java", "Programming");

Stream<String> mergedStream = Stream.of(stream1, stream2)
    .flatMap(Function.identity());

mergedStream.forEach(System.out::println);
```

这会输出：

```java
Hello
World
Java
Programming
```

在这个示例中，我们使用`flatMap`合并了`stream1`和`stream2`，并通过`Function.identity()`函数将它们扁平化。

**示例2：元素转换**

假设你有一个字符串流，想将每个字符串拆分为单词并得到单词的流：

```java
Stream<String> stringStream = Stream.of("Hello World", "Java Programming");

Stream<String> wordStream = stringStream
    .flatMap(str -> Stream.of(str.split(" ")));

wordStream.forEach(System.out::println);
```

这会输出：

```java
Hello
World
Java
Programming
```

在这个示例中，我们使用`flatMap`将每个字符串分割为单词，并将它们合并成一个单词流。

**示例3：扁平化嵌套集合**

假设你有一个包含多个子集合的集合，想将它们扁平化为单一流：

```java
List<List<Integer>> nestedList = Arrays.asList(
    Arrays.asList(1, 2, 3),
    Arrays.asList(4, 5),
    Arrays.asList(6, 7, 8)
);

Stream<Integer> flattenedStream = nestedList
    .stream()
    .flatMap(List::stream);

flattenedStream.forEach(System.out::println);
```

这会输出：

```java
1
2
3
4
5
6
7
8
```

在这个示例中，我们使用`flatMap`将嵌套的列表转换为单一流，以便更容易处理其中的元素。

## 7.5 实例

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.IntSummaryStatistics;
import java.util.List;
import java.util.Random;
import java.util.stream.Collectors;
import java.util.Map;

public class StreamTest {
    public static void main(String args[]) {
        System.out.println("Using Java 7: ");

        // 统计空字符串的数量
        List<String> strings = Arrays.asList("efg", "", "abc", "bc", "ghij", "", "lmn");
        System.out.println("List: " + strings);
        long count = getCountEmptyStringUsingJava7(strings);

        System.out.println("Empty Strings: " + count);
        count = getCountLength3UsingJava7(strings);

        System.out.println("Strings of length 3: " + count);

        // 消除空字符串
        List<String> filtered = deleteEmptyStringsUsingJava7(strings);
        System.out.println("Filtered List: " + filtered);

        // 消除空字符串，同时使用逗号来连接
        String mergedString = getMergedStringUsingJava7(strings, ", ");
        System.out.println("Merged String: " + mergedString);
        List<Integer> numbers = Arrays.asList(2, 3, 3, 2, 5, 2, 7);

        // 获得不同数字的平方的列表
        List<Integer> squaresList = getSquares(numbers);
        System.out.println("Squares List: " + squaresList);
        List<Integer> integers = Arrays.asList(1, 2, 13, 4, 15, 6, 17, 8, 19);

        System.out.println("List: " + integers);
        System.out.println("Highest number in List : " + getMax(integers));
        System.out.println("Lowest number in List : " + getMin(integers));
        System.out.println("Sum of all numbers : " + getSum(integers));
        System.out.println("Average of all numbers : " + getAverage(integers));

        // 输出10个随机数
        System.out.println("Random Numbers: ");
        Random random = new Random();

        for (int i = 0; i < 10; i++) {
            System.out.println(random.nextInt());
        }

        // 使用Java 8的新特性

        System.out.println("Using Java 8: ");
        System.out.println("List: " + strings);

        count = strings.stream().filter(string -> string.isEmpty()).count();
        System.out.println("Empty Strings: " + count);

        count = strings.stream().filter(string -> string.length() == 3).count();
        System.out.println("Strings of length 3: " + count);

        filtered = strings.stream().filter(string -> !string.isEmpty()).collect(Collectors.toList());
        System.out.println("Filtered List: " + filtered);

        mergedString = strings.stream().filter(string -> !string.isEmpty()).collect(Collectors.joining(", "));
        System.out.println("Merged String: " + mergedString);

        squaresList = numbers.stream().map(i -> i * i).distinct().collect(Collectors.toList());
        System.out.println("Squares List: " + squaresList);
        System.out.println("List: " + integers);

        IntSummaryStatistics stats = integers.stream().mapToInt((x) -> x).summaryStatistics();

        // 输出结果
        System.out.println("Highest number in List : " + stats.getMax());
        System.out.println("Lowest number in List : " + stats.getMin());
        System.out.println("Sum of all numbers : " + stats.getSum());
        System.out.println("Average of all numbers : " + stats.getAverage());
        System.out.println("Random Numbers: ");

        random.ints().limit(10).sorted().forEach(System.out::println);

        // 并行处理
        count = strings.parallelStream().filter(string -> string.isEmpty()).count();
        System.out.println("Empty Strings: " + count);
    }

    // 使用Java 7版本就提供的API来计算空串数量
    private static int getCountEmptyStringUsingJava7(List<String> strings) {
        int count = 0;

        for (String string : strings) {

            if (string.isEmpty()) {
                count++;
            }
        }
        return count;
    }

    // 使用Java 7版本就提供的API来计算长度为3字符的字符串数量
    private static int getCountLength3UsingJava7(List<String> strings) {
        int count = 0;

        for (String string : strings) {

            if (string.length() == 3) {
                count++;
            }
        }
        return count;
    }

    // 使用Java 7版本就提供的API来删除空串
    private static List<String> deleteEmptyStringsUsingJava7(List<String> strings) {
        List<String> filteredList = new ArrayList<String>();

        for (String string : strings) {

            if (!string.isEmpty()) {
                filteredList.add(string);
            }
        }
        return filteredList;
    }

    // 使用Java 7版本就提供的API来获取合并后的字符串
    private static String getMergedStringUsingJava7(List<String> strings, String separator) {
        StringBuilder stringBuilder = new StringBuilder();

        for (String string : strings) {

            if (!string.isEmpty()) {
                stringBuilder.append(string);
                stringBuilder.append(separator);
            }
        }
        String mergedString = stringBuilder.toString();
        return mergedString.substring(0, mergedString.length() - 2);
    }

    // 自定义的用于计算数字的平方的方法
    private static List<Integer> getSquares(List<Integer> numbers) {
        List<Integer> squaresList = new ArrayList<Integer>();

        for (Integer number : numbers) {
            Integer square = new Integer(number.intValue() * number.intValue());

            if (!squaresList.contains(square)) {
                squaresList.add(square);
            }
        }
        return squaresList;
    }

    // 自定义的用于获得List中最大值的方法
    private static int getMax(List<Integer> numbers) {
        int max = numbers.get(0);

        for (int i = 1; i < numbers.size(); i++) {

            Integer number = numbers.get(i);

            if (number.intValue() > max) {
                max = number.intValue();
            }
        }
        return max;
    }

    // 自定义的用于获得List中最小值的方法
    private static int getMin(List<Integer> numbers) {
        int min = numbers.get(0);

        for (int i = 1; i < numbers.size(); i++) {
            Integer number = numbers.get(i);

            if (number.intValue() < min) {
                min = number.intValue();
            }
        }
        return min;
    }

    // 自定义的用于获得List中各个数字的和的方法
    private static int getSum(List<Integer> numbers) {
        int sum = (int) (numbers.get(0));

        for (int i = 1; i < numbers.size(); i++) {
            sum += (int) numbers.get(i);
        }
        return sum;
    }

    // 自定义的用于获得List中各个数字的平均值的方法
    private static int getAverage(List<Integer> numbers) {
        return getSum(numbers) / numbers.size();
    }
}
```

# 8 IO

## 8.1 文件

`java.io.File` 类是 Java 中用于操作文件和目录的基本类之一。它允许你创建、删除、重命名、查询文件和目录的属性等操作。以下是一些常见的 `File` 类的用法和示例：

1. 创建 `File` 对象：

   - 通过指定文件或目录的路径来创建 `File` 对象。

   ```java
   File file = new File("/path/to/file.txt");
   File directory = new File("/path/to/directory");
   ```

2. 检查文件或目录是否存在：

   - 使用 `exists()` 方法检查文件或目录是否存在。

   ```java
   boolean exists = file.exists();
   ```

3. 创建文件或目录：

   - 使用 `createNewFile()` 方法创建文件。

   ```java
   boolean created = file.createNewFile();
   ```

   - 使用 `mkdir()` 方法创建目录。

   ```java
   boolean created = directory.mkdir();
   ```

4. 删除文件或目录：

   - 使用 `delete()` 方法删除文件或目录。

   ```java
   boolean deleted = file.delete();
   ```

5. 获取文件或目录的属性：

   - 使用 `getName()` 方法获取文件或目录的名称。

   ```java
   String name = file.getName();
   ```

   - 使用 `isFile()` 和 `isDirectory()` 方法检查文件或目录的类型。

   ```java
   boolean isFile = file.isFile();
   boolean isDirectory = directory.isDirectory();
   ```

6. 获取文件大小和最后修改时间：

   - 使用 `length()` 方法获取文件大小（字节数）。

   ```java
   long fileSize = file.length();
   ```

   - 使用 `lastModified()` 方法获取文件的最后修改时间戳。

   ```java
   long lastModifiedTime = file.lastModified();
   ```

7. 列出目录中的文件和子目录：

   - 使用 `list()` 方法获取目录中的所有文件和子目录的名称。

   ```java
   String[] contents = directory.list();
   ```

   - 使用 `listFiles()` 方法获取目录中的所有文件和子目录的 `File` 对象。

   ```java
   File[] files = directory.listFiles();
   ```

8. 重命名文件或目录：

   - 使用 `renameTo()` 方法重命名文件或目录。

   ```java
   File newFile = new File("/path/to/new_name.txt");
   boolean renamed = file.renameTo(newFile);
   ```

## 8.2 文件流

文件输入流（FileInputStream）：

1. 导入必要的输入输出流类：

   ```java
   import java.io.FileInputStream;
   import java.io.IOException;
   ```

2. 创建 `FileInputStream` 对象并打开文件：

   ```java
   FileInputStream fileInputStream = new FileInputStream("path/to/your/file.txt");
   ```

3. 读取文件内容：

   - 使用 `read()` 方法逐个字节读取文件内容。

   ```java
   int data;
   while ((data = fileInputStream.read()) != -1) {
       // 处理读取到的字节数据，可以将其转换成字符或做其他处理
       char character = (char) data;
       System.out.print(character);
   }
   ```

4. 关闭文件输入流：

   ```java
   fileInputStream.close();
   ```

文件输出流（FileOutputStream）：

1. 导入必要的输入输出流类：

   ```java
   import java.io.FileOutputStream;
   import java.io.IOException;
   ```

2. 创建 `FileOutputStream` 对象并打开文件：

   ```java
   FileOutputStream fileOutputStream = new FileOutputStream("path/to/your/output/file.txt");
   ```

3. 写入数据到文件：

   - 使用 `write()` 方法写入字节数组到文件。

   ```java
   String text = "Hello, world!";
   byte[] bytes = text.getBytes();
   fileOutputStream.write(bytes);
   ```

4. 关闭文件输出流：

   ```java
   fileOutputStream.close();
   ```

3.`BufferedReader` 是 Java 中的一个字符缓冲输入流类，它用于高效读取文本文件的内容。它通常与其他字符输入流一起使用，如 `FileReader` 或 `InputStreamReader`，以提高读取性能和效率。

`BufferedReader` 具有以下主要特点和功能：

1. 缓冲机制：`BufferedReader` 在内部维护一个缓冲区，可以一次性读取多个字符，然后逐个提供给程序。这减少了频繁的磁盘或网络访问，从而提高了读取效率。
2. 逐行读取：`BufferedReader` 提供了 `readLine()` 方法，允许你逐行读取文本文件的内容，这在处理文本文件时非常常见。
3. 自动字符编码：`BufferedReader` 默认会根据系统的字符编码自动处理字符解码，这意味着它可以正确处理不同字符编码的文本文件。
4. 提供字符数组读取：除了逐行读取外，你还可以使用 `read(char[] cbuf, int off, int len)` 方法来读取指定数量的字符到字符数组中。
5. 支持跳过字符：它还提供了 `skip(long n)` 方法，允许你跳过指定数量的字符。

以下是创建和使用 `BufferedReader` 的基本示例：

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class BufferedReaderExample {
    public static void main(String[] args) {
        try {
            FileReader fileReader = new FileReader("path/to/your/textfile.txt");
            BufferedReader bufferedReader = new BufferedReader(fileReader);
            
            String line;
            while ((line = bufferedReader.readLine()) != null) {
                // 处理每一行文本数据
                System.out.println(line);
            }
            
            bufferedReader.close();
            fileReader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

在上面的示例中，我们使用了 `BufferedReader` 来逐行读取文本文件的内容，并确保在使用完毕后关闭流以释放资源。

## 8. 3 RandomAccessFile

`RandomAccessFile` 是 Java 中用于随机访问文件的类，它允许你在文件中定位特定的位置并读取或写入数据。你可以使用 `RandomAccessFile` 执行以下操作：

1. 打开文件：使用 `RandomAccessFile` 的构造函数来打开文件，并指定文件名和打开模式（只读、读写等）。
2. 定位文件指针：使用 `seek()` 方法来定位文件中的指针位置，以便读取或写入数据。
3. 读取数据：使用 `read()` 方法来从文件中读取数据。
4. 写入数据：使用 `write()` 方法来向文件中写入数据。
5. 关闭文件：在完成操作后，使用 `close()` 方法关闭文件。

以下是一个示例，演示如何使用 `RandomAccessFile` 来读取和写入文件：

```java
import java.io.RandomAccessFile;
import java.io.IOException;

public class RandomAccessFileExample {
    public static void main(String[] args) {
        try {
            // 打开文件，使用 "rw" 表示读写模式
            RandomAccessFile file = new RandomAccessFile("path/to/your/file.txt", "rw");

            // 定位文件指针到特定位置
            file.seek(10); // 将文件指针定位到第11个字节的位置

            // 读取数据
            byte[] data = new byte[20];
            int bytesRead = file.read(data); // 从当前文件指针位置读取20个字节的数据
            System.out.println(new String(data, 0, bytesRead)); // 将读取的数据转换为字符串并输出

            // 写入数据
            file.seek(30); // 将文件指针定位到第31个字节的位置
            String newData = "New data to write.";
            file.write(newData.getBytes());

            // 关闭文件
            file.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

在上面的示例中，我们使用 `RandomAccessFile` 打开文件，定位文件指针，读取数据，写入数据，然后关闭文件。请注意，在实际应用中，你需要处理可能抛出的 `IOException` 异常，并确保在不再需要访问文件时关闭文件，以释放资源。

```java
import java.io.RandomAccessFile;

public class FileDemo {
    public static void main(String[] args) {
        int[] data_arr = {12, 32, 43, 45, 1, 5};

        try {
            // 打开一个名为 "temp.txt" 的文件，以读写模式打开
            RandomAccessFile randomAccessFile = new RandomAccessFile("temp.txt", "rw");

            // 循环遍历整数数组并将每个整数写入文件
            for(int i = 0; i < data_arr.length; i++){
                randomAccessFile.writeInt(data_arr[i]);
            }

            // 从文件中逆序读取整数并打印它们
            for(int i = data_arr.length-1; i >= 0; i--){
                // 定位文件指针到正确的位置，每个整数占用 4 个字节
                randomAccessFile.seek(i * 4L);
                
                // 读取整数并打印
                System.out.println(randomAccessFile.readInt());
            }

            // 关闭文件
            randomAccessFile.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

## 8.4 Files工具类

以下是一些常见的 `Files` 工具类的用法：

1. 复制文件或目录：

   ```java
   Path source = Paths.get("source.txt");
   Path target = Paths.get("target.txt");
   Files.copy(source, target, StandardCopyOption.REPLACE_EXISTING);
   ```

2. 移动文件或目录：

   ```java
   Path source = Paths.get("source.txt");
   Path target = Paths.get("new_directory/target.txt");
   Files.move(source, target, StandardCopyOption.REPLACE_EXISTING);
   ```

3. 删除文件或目录：

   ```java
   Path path = Paths.get("file_or_directory_to_delete.txt");
   Files.delete(path);
   ```

4. 创建文件：

   ```java
   Path file = Paths.get("new_file.txt");
   Files.createFile(file);
   ```

5. 创建目录：

   ```java
   Path directory = Paths.get("new_directory");
   Files.createDirectory(directory);
   ```

6. 创建多层次目录：

   ```java
   Path directories = Paths.get("parent_directory/child_directory");
   Files.createDirectories(directories);
   ```

7. 读取文件内容：

   ```java
   Path file = Paths.get("file.txt");
   List<String> lines = Files.readAllLines(file, StandardCharsets.UTF_8);
   ```

8. 写入文件内容：

   ```java
   Path file = Paths.get("file.txt");
   List<String> lines = Arrays.asList("Line 1", "Line 2", "Line 3");
   Files.write(file, lines, StandardCharsets.UTF_8);
   ```

9. 检查文件或目录是否存在：

   ```java
   Path path = Paths.get("file_or_directory.txt");
   boolean exists = Files.exists(path);
   ```

10. 获取文件属性：

    ```java
    Path file = Paths.get("file.txt");
    BasicFileAttributes attributes = Files.readAttributes(file, BasicFileAttributes.class);
    ```

## 8.5 file

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.nio.file.StandardCopyOption;

public class CopyDemo {
    public static void main(String[] args) {
        try {
            //被拷贝的文件一定要存在 否则会抛出异常  这里的1.txt一定要存在
            Files.copy(Paths.get("/home/project/1.txt"), Paths.get("/home/project/2.txt"), StandardCopyOption.REPLACE_EXISTING);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.nio.file.StandardCopyOption;

public class MoveDemo {
    public static void main(String[] args) {
        try {
            //将1.txt 重命名为3.txt 如果只需要移动到不同的目录，文件名不变即可
            Files.move(Paths.get("/home/project/1.txt"), Paths.get("/home/project/3.txt"), StandardCopyOption.REPLACE_EXISTING);
        //将2.txt 重命名为4.txt 如果只需要移动到不同的目录，文件名不变即可
        Files.move(Paths.get("/home/project/2.txt"), Paths.get("/home/project/4.txt"), StandardCopyOption.REPLACE_EXISTING);
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}
```

```java
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class DeleteDemo {
    public static void main(String[] args) {
        try {
            //删除文件，文件必须存在，否则抛出异常
            Files.delete(Paths.get("/home/project/3.txt"));
            //删除文件，返回是否删除成功 即使文件不存在，也不会保存，直接返回false
            System.out.println(Files.deleteIfExists(Paths.get("/home/project/3.txt")));
            //或者使用File类的delete方法
            File file = new File("/home/project/4.txt");
            System.out.println(file.delete());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

```java
import java.io.File;
import java.util.Arrays;

public class FileInfo {
    public static void main(String[] args) {
        File file = new File("/home/project");
        System.out.println("文件或者目录名：" + file.getName());
        System.out.println("绝对路径：" + file.getAbsolutePath());
        System.out.println("父目录：" + file.getParent());
        System.out.println("文件路径：" + file.getPath());
        //判断文件是否是目录
        if (file.isDirectory()) {
            //打印目录中的文件
            Arrays.stream(file.list()).forEach(System.out::println);
        }
        System.out.println("是否隐藏：" + file.isHidden());
        System.out.println("是否存在：" + file.exists());
    }
}
```

```java
import java.io.File;

public class ReadDir {
    public static void main(String[] args) {
        // 调用readDir方法，传入指定目录的File对象
        readDir(new File("/home"));
    }

    /**
     * 递归地读取目录和文件，并输出它们的类型和名称
     *
     * @param file 要处理的File对象
     */
    public static void readDir(File file) {
        // 如果传入的File对象为null，则直接返回
        if (file == null) return;
        
        // 如果File对象表示一个目录
        if (file.isDirectory()) {
            // 输出目录的信息（名称）
            System.out.println("目录" + file.getName());
            
            // 获取目录下的所有文件和子目录
            File[] files = file.listFiles();
            
            // 遍历每一个文件或子目录并递归调用readDir方法
            for (File file2 : files) {
                readDir(file2);
            }
        } else {
            // 如果File对象表示一个文件，输出文件的信息（名称）
            System.out.println("文件" + file.getName());
        }
    }
}

```

## 8.6 分类

IO流分为字节流和字符流的分类是基于处理数据的单位和性质来划分的。

1. **字节流 (Byte Stream)**:
   - **处理单位**: 以字节（8位）为单位进行数据处理，适用于处理二进制数据或者文本文件。
   - **性质**: 字节流是原始的、底层的输入输出，直接操作字节数据。
   - **InputStream和OutputStream**: 主要使用`InputStream`和`OutputStream`类及其子类来实现字节流。例如，`FileInputStream`用于从文件读取字节，`FileOutputStream`用于写入字节到文件。
2. **字符流 (Character Stream)**:
   - **处理单位**: 以字符为单位进行数据处理，适用于处理文本数据。
   - **性质**: 字符流是高级的，能够按照字符编码方式处理数据，适合文本数据处理。
   - **Reader和Writer**: 主要使用`Reader`和`Writer`类及其子类来实现字符流。例如，`FileReader`用于从文件读取字符，`FileWriter`用于写入字符到文件。

字符流的存在是为了解决字节流在处理文本数据时可能会遇到字符编码的问题。字符流能够根据指定的字符编码（如UTF-8、ASCII等）将字符转换为字节，并且能够以字符为单位更好地处理文本数据，避免乱码等问题。

> ![image-20231009190751075](C:\Users\7878\AppData\Roaming\Typora\typora-user-images\image-20231009190751075.png)

## 8.7 缓冲流

在Java中，缓冲流用于提高读取和写入性能，通过将数据缓存到内存中来减少与磁盘或网络的交互次数。主要有`BufferedReader`和`BufferedWriter`用于字符流的缓冲，以及`BufferedInputStream`和`BufferedOutputStream`用于字节流的缓冲。以下是如何使用Java缓冲流的基本步骤：

1. **导入必要的类**： 首先，确保导入Java IO包中的相关类。根据您的需求，您需要导入以下类之一：

   - 对于字符流的缓冲：

     ```java
     import java.io.BufferedReader;
     import java.io.BufferedWriter;
     ```

   - 对于字节流的缓冲：

     ```java
     import java.io.BufferedInputStream;
     import java.io.BufferedOutputStream;
     ```

2. **创建底层流**： 首先，创建底层的输入流（如`FileInputStream`或`FileReader`）或输出流（如`FileOutputStream`或`FileWriter`），这些流将连接到缓冲流。

3. **创建缓冲流**： 使用底层流来创建缓冲流。例如，对于字符输入流：

   ```java
   BufferedReader bufferedReader = new BufferedReader(new FileReader("文件路径"));
   ```

   对于字符输出流：

   ```java
   BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter("文件路径"));
   ```

   对于字节输入流：

   ```java
   BufferedInputStream bufferedInputStream = new BufferedInputStream(new FileInputStream("文件路径"));
   ```

   对于字节输出流：

   ```java
   BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(new FileOutputStream("文件路径"));
   ```

4. **使用缓冲流**： 现在，您可以使用缓冲流来读取或写入数据，它们提供了一些方便的方法。例如，使用`readLine()`来逐行读取文本文件，或使用`write()`来写入数据。

   示例：

   ```java
   String line;
   while ((line = bufferedReader.readLine()) != null) {
       // 处理读取的行数据
       bufferedWriter.write(line);
       bufferedWriter.newLine(); // 写入换行符
   }
   ```

5. **关闭流**： 使用完缓冲流后，务必关闭它们以释放资源。可以使用`close()`方法来关闭流，它也会自动关闭底层的基本流。

   ```java
   bufferedReader.close();
   bufferedWriter.close();
   ```

6. **刷新流**（可选）： 如果您在写入数据后需要立即将数据刷新到磁盘或网络，请调用`flush()`方法。

   ```java
   bufferedWriter.flush();
   ```

## 8.8 ObjectStream

`ObjectInputStream` 和 `ObjectOutputStream` 是 Java 中用于序列化和反序列化对象的类。它们可以将对象转换为字节流以便于存储和传输，并在需要时将字节流还原为对象。以下是如何使用这两个类的基本示例：

**对象的序列化（写入）：**

```java
import java.io.*;

public class ObjectSerialization {
    public static void main(String[] args) {
        try (FileOutputStream fileOutputStream = new FileOutputStream("object.ser");
             ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream)) {

            // 创建一个对象
            Person person = new Person("Alice", 30);

            // 将对象序列化并写入文件
            objectOutputStream.writeObject(person);
            System.out.println("对象已成功序列化");

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**对象的反序列化（读取）：**

```java
import java.io.*;

public class ObjectDeserialization {
    public static void main(String[] args) {
        try (FileInputStream fileInputStream = new FileInputStream("object.ser");
             ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream)) {

            // 从文件中读取序列化的对象
            Person person = (Person) objectInputStream.readObject();
            System.out.println("对象已成功反序列化");
            System.out.println("Name: " + person.getName());
            System.out.println("Age: " + person.getAge());

        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

上述示例中，`Person` 类是一个简单的自定义类，用于演示对象的序列化和反序列化。在实际应用中，您可以替换成您需要序列化的自定义对象。

要成功序列化对象，确保被序列化的对象及其成员都是可序列化的。为此，您可以实现 `Serializable` 接口，并在需要的情况下自定义 `serialVersionUID` 字段以控制版本兼容性。

```java
public static class User implements Serializable {
        private String name;
        private String id;
        public User(String name, String id){
            this.id = id;
            this.name = name;
        }

        @Override 
        public String toString(){
            return "User =" + name + "\nid = " + id + "\n";
        }
    }
```

# 9 网络

## 9.1 HttpURLConnection

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class HttpClientExample {
    public static void main(String[] args) {
        try {
            // 创建一个URL对象，指定要发送HTTP GET请求的目标地址
            URL url = new URL("https://example.com");
            // 打开HTTP连接
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();

            // 设置HTTP请求方法为GET
            connection.setRequestMethod("GET");

            // 获取HTTP响应码
            int responseCode = connection.getResponseCode();

            if (responseCode == HttpURLConnection.HTTP_OK) {
                // 如果响应码为200，表示请求成功

                // 创建一个BufferedReader对象来读取响应内容
                BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
                String inputLine;
                StringBuilder content = new StringBuilder();

                // 逐行读取响应内容并存储在StringBuilder中
                while ((inputLine = in.readLine()) != null) {
                    content.append(inputLine);
                }
                in.close();

                // 打印响应内容
                System.out.println(content.toString());
            } else {
                // 如果响应码不为200，打印HTTP请求失败信息
                System.out.println("HTTP request failed with response code: " + responseCode);
            }
        } catch (Exception e) {
            // 捕获并打印任何异常
            e.printStackTrace();
        }
    }
}
```

## 9.2 InetAddress

`InetAddress` 是 Java 中用于表示 IP 地址的类。它提供了一种在网络应用程序中操作 IP 地址的方式。你可以使用 `InetAddress` 来获取主机名和 IP 地址之间的映射，以及执行网络通信时需要的地址解析。

以下是一些常见的 `InetAddress` 类的用法示例：

**获取本地主机的 InetAddress 对象**：

```java
InetAddress localHost = InetAddress.getLocalHost();
System.out.println("本地主机的主机名：" + localHost.getHostName());
System.out.println("本地主机的IP地址：" + localHost.getHostAddress());
```

**通过主机名获取 InetAddress 对象**：

```java
String hostname = "www.example.com";
InetAddress address = InetAddress.getByName(hostname);
System.out.println("主机名：" + address.getHostName());
System.out.println("IP地址：" + address.getHostAddress());
```

**获取主机的所有 IP 地址**：

```java
String hostname = "www.example.com";
InetAddress[] addresses = InetAddress.getAllByName(hostname);
for (InetAddress addr : addresses) {
    System.out.println("主机名：" + addr.getHostName());
    System.out.println("IP地址：" + addr.getHostAddress());
}
```

**检查主机是否可达**：

```java
String hostname = "www.example.com";
InetAddress address = InetAddress.getByName(hostname);
if (address.isReachable(5000)) {
    System.out.println("主机可达");
} else {
    System.out.println("主机不可达");
}
```

## 9.3 Socket

使用 Java 中的 `Socket` 进行网络编程涉及以下步骤：

1. **创建客户端套接字**：如果你要编写客户端应用程序，首先需要创建一个 `Socket` 对象，以便连接到远程服务器。使用以下代码创建客户端套接字：

   ```java
   String serverHost = "example.com";
   int serverPort = 8080;
   
   try {
       Socket socket = new Socket(serverHost, serverPort);
       // 现在你可以使用 socket 进行数据发送和接收
   } catch (IOException e) {
       e.printStackTrace();
   }
   ```

2. **创建服务器套接字**：如果你要编写服务器应用程序，首先需要创建一个 `ServerSocket` 对象，以便侦听客户端的连接请求。使用以下代码创建服务器套接字：

   ```java
   int serverPort = 8080;
   
   try {
       ServerSocket serverSocket = new ServerSocket(serverPort);
       // 服务器套接字现在正在侦听客户端的连接请求
   } catch (IOException e) {
       e.printStackTrace();
   }
   ```

3. **与套接字进行数据通信**：一旦套接字建立连接，你可以使用 `InputStream` 和 `OutputStream` 来在客户端和服务器之间进行数据传输。例如，客户端可以使用 `socket.getOutputStream()` 发送数据，服务器可以使用 `socket.getInputStream()` 接收数据。

   ```java
   // 客户端发送数据示例
   OutputStream outputStream = socket.getOutputStream();
   PrintWriter writer = new PrintWriter(outputStream);
   writer.println("Hello, Server!");
   writer.flush();
   
   // 服务器接收数据示例
   InputStream inputStream = socket.getInputStream();
   BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
   String clientMessage = reader.readLine();
   ```

4. **关闭套接字**：在通信完成后，务必关闭套接字以释放资源。通常在 `try-catch-finally` 块中进行套接字关闭操作。

   ```java
   try {
       // 关闭套接字
       socket.close();
   } catch (IOException e) {
       e.printStackTrace();
   }
   ```

## 9.4 ServerSocket

在 Java 中，`ServerSocket` 类用于创建服务器套接字，以侦听客户端的连接请求。一旦建立连接，就可以创建与客户端的通信套接字，允许数据交换。以下是使用 `ServerSocket` 的基本步骤：

1. **创建 ServerSocket 实例**：首先，实例化 `ServerSocket` 并指定服务器将侦听的端口号。

   ```java
   int serverPort = 8080;
   ServerSocket serverSocket = new ServerSocket(serverPort);
   ```

2. **等待客户端连接**：使用 `accept()` 方法等待客户端连接请求。此方法会阻塞，直到有客户端连接到服务器。

   ```java
   Socket clientSocket = serverSocket.accept();
   ```

3. **与客户端进行通信**：一旦客户端连接成功，就可以使用 `InputStream` 和 `OutputStream` 与客户端进行数据交换。

   ```java
   InputStream inputStream = clientSocket.getInputStream();
   OutputStream outputStream = clientSocket.getOutputStream();
   ```

4. **接收和发送数据**：使用 `InputStream` 从客户端接收数据，并使用 `OutputStream` 向客户端发送数据。

   ```java
   // 从客户端接收数据
   BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
   String clientMessage = reader.readLine();
   
   // 向客户端发送数据
   PrintWriter writer = new PrintWriter(outputStream);
   writer.println("Hello, Client!");
   writer.flush();
   ```

5. **关闭连接**：在通信完成后，关闭客户端套接字和服务器套接字。

   ```java
   clientSocket.close();
   serverSocket.close();
   ```

完整示例代码如下所示：

```java
import java.io.*;
import java.net.*;

public class ServerExample {

    public static void main(String[] args) {
        int serverPort = 8080;

        try {
            ServerSocket serverSocket = new ServerSocket(serverPort);

            System.out.println("Server listening on port " + serverPort);

            // 等待客户端连接
            Socket clientSocket = serverSocket.accept();
            System.out.println("Client connected: " + clientSocket.getInetAddress());

            // 获取输入流和输出流
            InputStream inputStream = clientSocket.getInputStream();
            OutputStream outputStream = clientSocket.getOutputStream();

            // 从客户端接收数据
            BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
            String clientMessage = reader.readLine();
            System.out.println("Received from client: " + clientMessage);

            // 向客户端发送数据
            PrintWriter writer = new PrintWriter(outputStream);
            writer.println("Hello, Client!");
            writer.flush();

            // 关闭套接字
            clientSocket.close();
            serverSocket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

服务端和客户端信息发送

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;

public class EchoServer {
    public static void main(String[] args) {
        try {
            // 创建服务器套接字并指定端口号 1080
            ServerSocket serverSocket = new ServerSocket(1080);

            // 等待客户端连接
            Socket client = serverSocket.accept();

            // 创建用于向客户端发送数据的 PrintWriter
            PrintWriter out = new PrintWriter(client.getOutputStream(), true);

            // 创建用于从客户端接收数据的 BufferedReader
            BufferedReader in = new BufferedReader(new InputStreamReader(client.getInputStream()));

            String userIn;
            // 循环读取客户端发送的数据
            while ((userIn = in.readLine()) != null) {
                System.out.println("收到客户端消息：" + userIn);

                // 发回客户端相同的消息
                out.println(userIn);
            }

            // 关闭套接字
            client.close();
            serverSocket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.Socket;
import java.util.Scanner;

public class EchoClient {
    public static void main(String[] args) {
        // 服务器主机名
        String hostname = "127.0.0.1";

        // 服务器端口
        int port = 1080;

        // 用于从用户获取输入的 Scanner 对象
        Scanner userIn = new Scanner(System.in);

        try {
            // 建立与服务器的 socket 连接
            Socket socket = new Socket(hostname, port);

            // 获取 socket 输出流，用于向服务器发送数据
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

            // 获取 socket 输入流，用于接收服务器返回的数据
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));

            String userInput;

            System.out.println("请输入信息：");

            // 当用户输入 "exit" 时退出循环
            while (!"exit".equals(userInput = userIn.nextLine())) {
                // 将用户输入发送到服务器
                out.println(userInput);

                // 从服务器接收并打印回应
                System.out.println("收到服务端回应:" + in.readLine());
            }

            // 关闭 socket 连接
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

# 10 多线程

## 10.1 实现

1. **继承Thread类**（`Thread1`类）：
   - 当一个类继承自`Thread`类时，它成为一个线程类，可以直接通过创建该类的对象并调用`start()`方法来启动线程。这是一种较为简单的方式，但有一个缺点，即Java不支持多重继承，因此如果一个类已经继承了其他类，就不能再继承`Thread`类。
2. **实现Runnable接口**（`Thread2`类）：
   - 如果一个类已经有了一个父类或者你想要更好地分离线程的行为和类本身的行为，那么你可以选择实现`Runnable`接口。这允许你将线程的任务独立出来，以实现更灵活的多线程编程。你需要创建一个实现`Runnable`接口的类，然后将该类的实例传递给一个`Thread`对象来启动线程。这种方式避免了单一继承的限制。

```java
public class CreateThread {

    public static void main(String[] args) {
        Thread1 thread1 = new Thread1();
        //声明一个Thread1对象，这个Thread1类继承自Thread类的

        Thread thread2 = new Thread(new Thread2());
        //传递一个匿名对象作为参数

        thread1.start();
        thread2.start();
        //启动线程
    }
}

class Thread1 extends Thread {
    @Override
    public void run() {
        //在run()方法中放入线程要完成的工作

        //这里我们把两个线程各自的工作设置为打印100次信息
        for (int i = 0; i < 100; ++i) {
            System.out.println("Hello! This is " + i);
        }

        //在这个循环结束后，线程便会自动结束
    }
}

class Thread2 implements Runnable {
    //与Thread1不同，如果当一个线程已经继承了另一个类时，就建议你通过实现Runnable接口来构造

    @Override
    public void run() {
        for (int i = 0; i < 100; ++i) {
            System.out.println("Thanks. There is " + i);
        }
    }
}
```

## 10.2 线程变量

线程变量（Thread-local variables）是一种在多线程编程中用于在不同线程之间存储独立数据的机制。每个线程都有自己独立的变量副本，而不会相互干扰。这对于需要在线程间隔离数据的场景非常有用。

在Java中，你可以使用`ThreadLocal`类来创建线程变量。以下是使用`ThreadLocal`的基本步骤以及如何使用线程变量：

1. **创建 ThreadLocal 对象**： 首先，你需要创建一个`ThreadLocal`对象，用于存储线程本地变量。

   ```java
   ThreadLocal<String> threadLocalVariable = new ThreadLocal<>();
   ```

2. **设置线程变量的值**： 使用`ThreadLocal`对象的`set()`方法可以设置当前线程的变量值。

   ```java
   threadLocalVariable.set("This is thread-local data.");
   ```

3. **获取线程变量的值**： 使用`ThreadLocal`对象的`get()`方法可以获取当前线程的变量值。

   ```java
   String data = threadLocalVariable.get();
   ```

4. **移除线程变量的值**（可选）： 你也可以使用`ThreadLocal`对象的`remove()`方法来移除当前线程的变量值。

   ```java
   threadLocalVariable.remove();
   ```

5. **示例代码**： 下面是一个示例，演示如何在多线程环境中使用`ThreadLocal`来存储线程本地数据：

   ```java
   public class ThreadLocalExample {
   
       private static ThreadLocal<String> threadLocalVariable = ThreadLocal.withInitial(() -> "Default Value");
   
       public static void main(String[] args) {
           // 设置线程1的变量值
           threadLocalVariable.set("Thread 1 Data");
   
           // 启动线程2并获取其变量值
           Thread thread2 = new Thread(() -> {
               String data = threadLocalVariable.get();
               System.out.println("Thread 2 Data: " + data);
           });
   
           thread2.start();
       }
   }
   ```

在这个示例中，线程1设置了线程变量的值，然后线程2在不影响线程1的情况下获取了自己的线程变量值。这样，每个线程都有自己独立的线程变量，互不干扰。线程变量通常用于保存线程特定的上下文信息或状态。

## 10.3 线程同步

线程同步是一种用于控制多个线程在共享资源上的访问以防止竞争条件和数据不一致性的机制。在Java中，你可以使用以下方式来实现线程同步：

**使用synchronized关键字**：

- 在方法上使用`synchronized`关键字，或者在代码块内使用`synchronized`关键字，可以确保只有一个线程可以访问被标记为`synchronized`的方法或代码块。这种方式常用于同步对象的访问。

```java
public synchronized void synchronizedMethod() {
    // 同步的方法内容
}
```

```java
synchronized (lockObject) {
    // 同步的代码块
}
```

```java
public class SynchronizedExample {

    private int counter = 0;

    public synchronized void increment() {
        counter++;
    }

    public synchronized int getCounter() {
        return counter;
    }

    public static void main(String[] args) {
        SynchronizedExample example = new SynchronizedExample();

        // 创建多个线程并启动它们
        Thread thread1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                example.increment();
            }
        });

        Thread thread2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                example.increment();
            }
        });

        thread1.start();
        thread2.start();

        try {
            // 等待两个线程执行完毕
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // 输出最终计数器的值
        System.out.println("Final Counter Value: " + example.getCounter());
    }
}

```

**使用ReentrantLock**：

- `java.util.concurrent.locks.ReentrantLock`是一个更灵活的同步机制，可以用于替代`synchronized`关键字。它提供了更多的控制选项，如尝试获取锁、设置锁超时等。

```java
private final ReentrantLock lock = new ReentrantLock();

public void synchronizedMethod() {
    lock.lock();
    try {
        // 同步的方法内容
    } finally {
        lock.unlock();
    }
}
```

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class ReentrantLockExample {

    private int counter = 0;
    private Lock lock = new ReentrantLock(); // 创建一个ReentrantLock对象

    public void increment() {
        lock.lock(); // 获取锁
        try {
            counter++;
        } finally {
            lock.unlock(); // 释放锁
        }
    }

    public int getCounter() {
        lock.lock(); // 获取锁
        try {
            return counter;
        } finally {
            lock.unlock(); // 释放锁
        }
    }

    public static void main(String[] args) {
        ReentrantLockExample example = new ReentrantLockExample();

        // 创建多个线程并启动它们
        Thread thread1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                example.increment();
            }
        });

        Thread thread2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                example.increment();
            }
        });

        thread1.start();
        thread2.start();

        try {
            // 等待两个线程执行完毕
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // 输出最终计数器的值
        System.out.println("Final Counter Value: " + example.getCounter());
    }
}
```

在多线程编程中，`thread.join()` 是一个用于等待线程完成的方法。当一个线程调用另一个线程的 `join()` 方法时，它会被阻塞，直到被调用的线程执行完毕。这意味着程序会等待被调用的线程完成它的任务，然后再继续执行接下来的代码。

通常情况下，`thread.join()` 用于确保主线程等待所有其他线程完成之后再继续执行，这对于需要协调多个线程之间的操作非常有用。例如，如果你有一个主线程和多个工作线程，你可以使用 `join()` 来等待所有工作线程完成它们的任务，然后再进行结果的汇总或其他操作。

在Java中，`Condition` 是在多线程编程中用于控制线程之间协作和同步的一种机制。`Condition` 通常与 `ReentrantLock` 结合使用，以替代传统的 `synchronized` 块来实现更灵活的线程同步。

`Condition` 提供了类似于 `wait()` 和 `notify()` 方法的功能，但比它们更灵活。下面是一些关于 `Condition` 的基本用法：

1. 创建 `Condition`： 通常，你需要与一个 `ReentrantLock` 关联来创建一个 `Condition`。这可以通过调用 `ReentrantLock` 的 `newCondition()` 方法来实现。例如：

   ```java
   ReentrantLock lock = new ReentrantLock();
   Condition condition = lock.newCondition();
   ```

2. 等待条件： 你可以使用 `await()` 方法来让线程等待某个条件变为真。线程将被阻塞，直到其他线程调用 `signal()` 或 `signalAll()` 来通知等待的线程条件已满足。例如：

   ```java
   lock.lock();
   try {
       while (conditionNotMet) {
           condition.await();
       }
       // 执行条件已满足时的操作
   } finally {
       lock.unlock();
   }
   ```

3. 通知条件： 当某个条件发生变化时，可以使用 `signal()` 或 `signalAll()` 方法来通知等待的线程。`signal()` 通知一个等待线程，而 `signalAll()` 通知所有等待线程。例如：

   ```java
   lock.lock();
   try {
       // 更新条件
       conditionNotMet = false;
       // 通知等待的线程条件已满足
       condition.signal();
   } finally {
       lock.unlock();
   }
   ```

`Condition` 的使用允许更细粒度的线程同步，因为你可以选择哪个条件需要等待或被通知，而不是像传统的 `wait()` 和 `notify()` 那样只能等待或通知一个条件。这使得线程的管理和同步更加灵活和精确。

需要注意的是，`Condition` 通常与 `ReentrantLock` 配合使用，而不是与传统的 `synchronized` 关键字。这是因为 `Condition` 提供了更多的控制权和灵活性，适用于更复杂的多线程场景。

```java
import java.util.LinkedList;
import java.util.Queue;
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;

public class ProducerConsumerExample {
    private static final int CAPACITY = 5;  // 缓冲区容量
    private final Queue<Integer> buffer = new LinkedList<>();  // 缓冲区队列
    private final ReentrantLock lock = new ReentrantLock();  // 重入锁
    private final Condition notFull = lock.newCondition();  // 缓冲区不满的条件
    private final Condition notEmpty = lock.newCondition();  // 缓冲区不空的条件

    // 生产者方法：往缓冲区中添加数据
    public void produce(int item) throws InterruptedException {
        lock.lock();  // 获取锁
        try {
            while (buffer.size() == CAPACITY) {
                System.out.println("Buffer is full. Producer is waiting.");
                notFull.await();  // 缓冲区已满，生产者等待
            }
            buffer.offer(item);
            System.out.println("Produced: " + item);
            notEmpty.signal();  // 通知等待的消费者
        } finally {
            lock.unlock();  // 释放锁
        }
    }

    // 消费者方法：从缓冲区中取出数据
    public int consume() throws InterruptedException {
        lock.lock();  // 获取锁
        try {
            while (buffer.isEmpty()) {
                System.out.println("Buffer is empty. Consumer is waiting.");
                notEmpty.await();  // 缓冲区为空，消费者等待
            }
            int item = buffer.poll();
            System.out.println("Consumed: " + item);
            notFull.signal();  // 通知等待的生产者
            return item;
        } finally {
            lock.unlock();  // 释放锁
        }
    }

    public static void main(String[] args) {
        ProducerConsumerExample example = new ProducerConsumerExample();

        // 创建生产者线程
        Thread producerThread = new Thread(() -> {
            try {
                for (int i = 1; i <= 10; i++) {
                    example.produce(i);
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        // 创建消费者线程
        Thread consumerThread = new Thread(() -> {
            try {
                for (int i = 1; i <= 10; i++) {
                    int item = example.consume();
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        producerThread.start();  // 启动生产者线程
        consumerThread.start();  // 启动消费者线程

        try {
            producerThread.join();  // 等待生产者线程结束
            consumerThread.join();  // 等待消费者线程结束
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

```



## 10.4 死锁

```java
public class DeadlockExample {
    public static void main(String[] args) {
        // 创建两个资源
        Object resource1 = new Object();
        Object resource2 = new Object();

        // 线程1尝试获取资源1，然后资源2
        Thread thread1 = new Thread(() -> {
            synchronized (resource1) {
                System.out.println("Thread 1: Holding resource 1...");

                try {
                    Thread.sleep(100); // 为了增加死锁发生的机会
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }

                System.out.println("Thread 1: Waiting for resource 2...");
                synchronized (resource2) {
                    System.out.println("Thread 1: Acquired resource 2.");
                }
            }
        });

        // 线程2尝试获取资源2，然后资源1
        Thread thread2 = new Thread(() -> {
            synchronized (resource2) {
                System.out.println("Thread 2: Holding resource 2...");

                try {
                    Thread.sleep(100); // 为了增加死锁发生的机会
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }

                System.out.println("Thread 2: Waiting for resource 1...");
                synchronized (resource1) {
                    System.out.println("Thread 2: Acquired resource 1.");
                }
            }
        });

        // 启动两个线程
        thread1.start();
        thread2.start();

        // 等待两个线程完成
        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Both threads have finished.");
    }
}
```

## 10.5  ArrayBlockingQueue

`ArrayBlockingQueue` 是 Java 标准库中的一个有界阻塞队列，用于多线程编程中的生产者-消费者问题或其他线程协作场景。它基于数组实现，具有固定的容量，并且当队列已满时，生产者将被阻塞，当队列为空时，消费者将被阻塞。这种队列的特性使得它适用于限制资源的共享。

以下是如何创建和使用 `ArrayBlockingQueue` 的基本示例：

导入 `java.util.concurrent` 包：

```java
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;
```

创建 `ArrayBlockingQueue` 对象，并指定队列容量：

```java
BlockingQueue<Integer> queue = new ArrayBlockingQueue<>(10); // 创建容量为10的队列
```

在生产者线程中往队列中添加元素，可以使用 `put()` 方法来添加，如果队列已满，它将等待：

```java
try {
    queue.put(1); // 将元素1放入队列
} catch (InterruptedException e) {
    // 处理异常
}
```

在消费者线程中从队列中取出元素，可以使用 `take()` 方法来取出，如果队列为空，它将等待：

```java
try {
    int item = queue.take(); // 从队列中取出元素
    // 处理取出的元素
} catch (InterruptedException e) {
    // 处理异常
}
```

你还可以使用 `offer()` 方法尝试往队列中添加元素，如果队列已满，它会立即返回 `false`，或者使用 `poll()` 方法尝试取出元素，如果队列为空，它会立即返回 `null`。

```java
boolean added = queue.offer(2); // 尝试将元素2放入队列，如果队列已满返回false
Integer item = queue.poll(); // 尝试从队列中取出元素，如果队列为空返回null
```

`ArrayBlockingQueue` 还提供了其他一些方法，如 `offer(E e, long timeout, TimeUnit unit)` 和 `poll(long timeout, TimeUnit unit)`，它们允许你在超时时间内尝试添加或取出元素。此外，你还可以使用 `remainingCapacity()` 方法来获取队列中剩余可用空间的数量。

## 10.6 生产消费者

```java
import java.util.Random;
import java.util.concurrent.LinkedBlockingQueue;

public class PCModel {
    private static LinkedBlockingQueue<Integer> queue = new LinkedBlockingQueue<>();
    String[] arr = {"生产一", "生产二", "消费一", "消费二"};
    public static void main(String[] args) {
        PCModel pcModel = new PCModel();

        Provider provider1 = pcModel.new Provider();
        Thread threadProvider1 = new Thread(provider1);
        
        Consumer consumer1 = pcModel.new Consumer();
        Thread threadConsumer1 = new Thread(consumer1);
        
        Provider provider2 = pcModel.new Provider();
        Thread threadProvider2 = new Thread(provider2);
        
        Consumer consumer2 = pcModel.new Consumer();
        Thread threadConsumer2 = new Thread(consumer2);
        
        provider1.setS1("生产一");
        consumer1.setS1("消费一");
        provider2.setS1("生产二");
        consumer2.setS1("消费二");

        try {
            Thread.sleep(500);
        } catch (InterruptedException e) {
            
            e.printStackTrace();
        }
        threadProvider1.start();
        threadConsumer1.start();
        threadProvider2.start();
        threadConsumer2.start();
    }

    class Provider  implements Runnable {
        ThreadLocal<String> s = new ThreadLocal<>();
        private String s1;
        public void setS(String str) {
            s.set(str);
        }

        public void setS1(String str){
            this.s1 = str;
        }

        @Override
        public void run() {
            for(int i = 1; i <= 5; i++) {
                Integer integer = new Random().nextInt(100);
                queue.add(integer);
                System.out.println(s1 + "制做了" + integer);
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    class Consumer implements Runnable {
        ThreadLocal<String> s = new ThreadLocal<>();
        private String s2;

        public void setS(String str) {
            s.set(str);
        }

        public void setS1(String str){
            this.s2 = str;
        }


        @Override
        public void run() {
            
            for(int i = 1; i <= 5; i++) {
                while(queue.size() == 0) {
                    System.out.println(s2 + "正在等待");
                    try {
                        Thread.sleep(500);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                Integer integer;
                try {
                    integer = queue.take();
                    System.out.println(s2 + "获取了" + integer);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

```

## 10.7 线程池

线程池是一种用于管理和重用线程的机制，它可以帮助你更有效地管理多线程任务，减少线程的创建和销毁开销。Java 提供了 `java.util.concurrent` 包，其中包含了线程池的实现，使其在多线程应用程序中更容易使用。

下面是如何在Java中使用线程池的一般步骤：

1. 创建线程池：你可以使用 `ExecutorService` 接口的工厂方法来创建线程池，通常有以下几种类型：
   - `Executors.newFixedThreadPool(int nThreads)`: 创建一个具有固定线程数的线程池，线程数不会变化。
   - `Executors.newCachedThreadPool()`: 创建一个具有可根据需要创建新线程的线程池，适用于短期异步任务。
   - `Executors.newSingleThreadExecutor()`: 创建一个仅包含一个线程的线程池，用于按顺序执行任务。
   - `Executors.newScheduledThreadPool(int corePoolSize)`: 创建一个固定大小的线程池，用于调度定时任务。
2. 提交任务：使用线程池的 `submit` 或 `execute` 方法提交需要执行的任务。
3. 关闭线程池：当不再需要线程池时，应该调用线程池的 `shutdown` 或 `shutdownNow` 方法来关闭线程池。这将停止线程池中的所有线程并释放资源。

以下是一个简单示例：

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadPoolExample {
    public static void main(String[] args) {
        // 创建一个固定大小为3的线程池
        ExecutorService threadPool = Executors.newFixedThreadPool(3);

        // 提交任务给线程池
        for (int i = 1; i <= 5; i++) {
            final int task = i;
            threadPool.submit(() -> {
                System.out.println("Task " + task + " is executing by thread " + Thread.currentThread().getId());
            });
        }

        // 关闭线程池
        threadPool.shutdown();
    }
}
```

在这个示例中，我们创建了一个固定大小为3的线程池，然后提交了5个任务。线程池会自动分配任务给可用的线程，执行完任务后关闭线程池。

使用线程池可以提高多线程应用程序的性能和可维护性，因为它可以避免频繁创建和销毁线程，以及管理线程的生命周期。

# 11 JDBC

## 11.1 JDBC

JDBC 是 Java Database Connectivity 的缩写，是 Java 编程语言用于与关系型数据库进行连接和交互的标准 API（应用程序接口）。JDBC 允许 Java 应用程序通过标准接口访问和操作数据库，而不依赖于特定数据库系统。

JDBC 提供了一组类和接口，使开发人员能够执行以下任务：

1. 建立数据库连接：通过 JDBC，你可以创建与数据库的连接，这通常涉及到提供数据库的连接 URL、用户名和密码。
2. 执行 SQL 查询：你可以使用 JDBC 来执行 SQL 查询，包括 SELECT 查询用于检索数据和 INSERT、UPDATE、DELETE 查询用于修改数据。
3. 处理结果集：JDBC 允许你从数据库中检索查询结果，并将结果封装为 Java 对象，以便在应用程序中处理。
4. 处理事务：JDBC 支持事务处理，你可以使用它来控制多个 SQL 操作的原子性和一致性。
5. 处理异常：JDBC 引发异常来处理各种数据库操作可能遇到的问题，开发人员可以捕获和处理这些异常以实现错误处理和故障恢复。

JDBC 是一种非常强大和灵活的工具，它允许 Java 应用程序与各种关系型数据库（如Oracle、MySQL、SQL Server、PostgreSQL等）进行集成。使用 JDBC，开发人员可以编写数据库无关的代码，从而能够轻松切换和连接到不同的数据库系统，而不必修改应用程序的大部分代码。

JDBC 驱动程序是用于不同数据库系统的具体实现，它们充当 JDBC API 和数据库之间的桥梁，允许 Java 应用程序与特定数据库进行通信。常见的 JDBC 驱动程序包括MySQL Connector/J、Oracle JDBC 驱动程序等。开发人员需要根据使用的数据库系统选择合适的 JDBC 驱动程序来建立连接。

## 11.2 连接

使用Java中的JDBC（Java Database Connectivity）来连接和操作数据库通常需要以下步骤：

1. **导入JDBC库**：首先，你需要导入JDBC库，通常包括Java的`java.sql`包和特定数据库的JDBC驱动程序库。你可以通过在Java项目中添加JAR文件或使用Maven等构建工具来引入所需的JDBC库。

2. **加载数据库驱动程序**：在你的Java应用程序中，使用`Class.forName()`方法来加载特定数据库的JDBC驱动程序。不同的数据库有不同的驱动程序类名。例如，对于MySQL数据库，你可以加载MySQL的JDBC驱动程序如下：

   ```java
   Class.forName("com.mysql.cj.jdbc.Driver");
   ```

3. **建立数据库连接**：使用`DriverManager.getConnection()`方法来建立与数据库的连接。你需要提供数据库的连接字符串、用户名和密码。连接字符串的格式会根据使用的数据库类型而有所不同。例如，连接到MySQL数据库可以如下所示：

   ```java
   String url = "jdbc:mysql://localhost:3306/your_database";
   String username = "your_username";
   String password = "your_password";
   Connection connection = DriverManager.getConnection(url, username, password);
   ```

4. **创建和执行SQL语句**：使用`Connection`对象来创建`Statement`、`PreparedStatement`或`CallableStatement`对象，然后使用它们来执行SQL查询或更新操作。例如，执行一个简单的查询：

   ```java
   Statement statement = connection.createStatement();
   ResultSet resultSet = statement.executeQuery("SELECT * FROM your_table");
   while (resultSet.next()) {
       // 处理查询结果
   }
   ```

5. **处理结果**：如果你执行的是查询操作，你可以使用`ResultSet`对象来获取查询结果。如果执行的是更新操作，你可以检查受影响的行数。

6. **关闭连接和资源**：使用完数据库连接和其他资源后，记得关闭它们，以释放资源并确保安全关闭。通常，你需要在`finally`块中关闭连接、语句和结果集。

   ```java
   if (resultSet != null) {
       resultSet.close();
   }
   if (statement != null) {
       statement.close();
   }
   if (connection != null) {
       connection.close();
   }
   ```

7. **异常处理**：务必处理可能抛出的异常，以确保程序的健壮性。你可以使用`try-catch`块来捕获异常。

## 11.3 Statement

1. **execute(String sql)** 示例：

   ```java
   Statement statement = connection.createStatement();
   boolean isResultSet = statement.execute("SELECT * FROM your_table");
   if (isResultSet) {
       ResultSet resultSet = statement.getResultSet();
       // 处理查询结果...
   } else {
       int rowsAffected = statement.getUpdateCount();
       System.out.println(rowsAffected + " rows updated.");
   }
   statement.close();
   ```

2. **executeQuery(String sql)** 示例：

   ```java
   Statement statement = connection.createStatement();
   ResultSet resultSet = statement.executeQuery("SELECT * FROM your_table");
   while (resultSet.next()) {
       int id = resultSet.getInt("id");
       String name = resultSet.getString("name");
       // 处理查询结果...
   }
   statement.close();
   ```

3. **executeUpdate(String sql)** 示例：

   ```java
   Statement statement = connection.createStatement();
   int rowsAffected = statement.executeUpdate("UPDATE your_table SET column1 = 'value' WHERE column2 = 'criteria'");
   System.out.println(rowsAffected + " rows updated.");
   statement.close();
   ```

4. **addBatch(String sql) 和 executeBatch() 示例**：

   ```java
   Statement statement = connection.createStatement();
   statement.addBatch("INSERT INTO your_table (column1, column2) VALUES ('value1', 'value2')");
   statement.addBatch("UPDATE your_table SET column1 = 'new_value' WHERE column2 = 'criteria'");
   int[] batchResults = statement.executeBatch();
   // 处理批处理结果...
   statement.close();
   ```

5. **setMaxRows(int max)** 示例：

   ```java
   Statement statement = connection.createStatement();
   statement.setMaxRows(10); // 限制结果集最多返回 10 行
   ResultSet resultSet = statement.executeQuery("SELECT * FROM your_table");
   while (resultSet.next()) {
       int id = resultSet.getInt("id");
       String name = resultSet.getString("name");
       // 处理查询结果...
   }
   statement.close();
   ```

## 11.4 PreparedStatement

> 1. **预编译性**：
>    - `Statement` 是动态 SQL 语句，每次执行 SQL 查询时，都需要将 SQL 字符串发送到数据库进行解析和编译。这可能会导致性能下降，特别是在频繁执行相同查询时。
>    - `PreparedStatement` 是预编译的 SQL 语句，它在数据库中已经编译好了。你可以在 SQL 语句中使用占位符（如 `?`），然后在执行时提供具体的值，而不需要重新编译 SQL 语句。这提高了性能并减少了潜在的 SQL 注入风险。
> 2. **SQL 注入**：
>    - `Statement` 在构造 SQL 查询时直接将变量值插入到查询字符串中，如果不谨慎处理输入数据，可能会导致 SQL 注入攻击。
>    - `PreparedStatement` 使用占位符来分离 SQL 查询和数据值，从而减少了 SQL 注入风险。数据库会安全处理占位符中的数据值。
> 3. **可读性和维护性**：
>    - `Statement` 可能会导致更复杂的 SQL 查询字符串，因为你需要手动将值嵌入到查询中。
>    - `PreparedStatement` 更容易维护，因为 SQL 查询和数据值是分开的。
> 4. **性能**：
>    - `PreparedStatement` 通常比 `Statement` 更快，特别是在重复执行相同的查询时，因为它允许数据库进行查询缓存和优化。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class PreparedStatementExample {
    private static final String JDBC_URL = "jdbc:mysql://localhost:3306/your_database";
    private static final String USERNAME = "your_username";
    private static final String PASSWORD = "your_password";

    public static void main(String[] args) {
        try {
            // 1. 创建数据库连接
            Connection connection = DriverManager.getConnection(JDBC_URL, USERNAME, PASSWORD);

            // 2. 插入数据
            insertData(connection, "john_doe", "john@example.com");

            // 3. 查询数据
            retrieveData(connection, "john_doe");

            // 4. 更新数据
            updateData(connection, "john_doe", "new_email@example.com");

            // 5. 删除数据
            deleteData(connection, "john_doe");

            // 6. 关闭连接
            connection.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // 插入数据
    private static void insertData(Connection connection, String username, String email) throws SQLException {
        String insertSQL = "INSERT INTO users (username, email) VALUES (?, ?)";
        PreparedStatement preparedStatement = connection.prepareStatement(insertSQL);
        preparedStatement.setString(1, username);
        preparedStatement.setString(2, email);
        int rowsInserted = preparedStatement.executeUpdate();
        System.out.println(rowsInserted + " row(s) inserted.");
        preparedStatement.close();
    }

    // 查询数据
    private static void retrieveData(Connection connection, String username) throws SQLException {
        String selectSQL = "SELECT * FROM users WHERE username = ?";
        PreparedStatement preparedStatement = connection.prepareStatement(selectSQL);
        preparedStatement.setString(1, username);
        ResultSet resultSet = preparedStatement.executeQuery();
        while (resultSet.next()) {
            System.out.println("User ID: " + resultSet.getInt("id"));
            System.out.println("Username: " + resultSet.getString("username"));
            System.out.println("Email: " + resultSet.getString("email"));
        }
        preparedStatement.close();
    }

    // 更新数据
    private static void updateData(Connection connection, String username, String newEmail) throws SQLException {
        String updateSQL = "UPDATE users SET email = ? WHERE username = ?";
        PreparedStatement preparedStatement = connection.prepareStatement(updateSQL);
        preparedStatement.setString(1, newEmail);
        preparedStatement.setString(2, username);
        int rowsUpdated = preparedStatement.executeUpdate();
        System.out.println(rowsUpdated + " row(s) updated.");
        preparedStatement.close();
    }

    // 删除数据
    private static void deleteData(Connection connection, String username) throws SQLException {
        String deleteSQL = "DELETE FROM users WHERE username = ?";
        PreparedStatement preparedStatement = connection.prepareStatement(deleteSQL);
        preparedStatement.setString(1, username);
        int rowsDeleted = preparedStatement.executeUpdate();
        System.out.println(rowsDeleted + " row(s) deleted.");
        preparedStatement.close();
    }
}

```

## 11.5 ResultSet

在 Java 中，你可以使用 `ResultSet` 对象来处理从数据库查询中获取的结果集。以下是一些常见的 `ResultSet` 操作：

1. **遍历结果集**：你可以使用 `while` 循环和 `resultSet.next()` 方法遍历结果集的每一行。在循环内部，你可以使用不同的 `getXXX` 方法来获取不同列的数据，例如 `getInt()`, `getString()`, `getDouble()` 等。

   ```java
   ResultSet resultSet = statement.executeQuery("SELECT * FROM my_table");
   while (resultSet.next()) {
       int id = resultSet.getInt("id");
       String name = resultSet.getString("name");
       // 处理每一行数据
   }
   ```

2. **获取单个列的数据**：你可以使用 `getXXX` 方法来获取单个列的数据，例如 `getInt()`, `getString()`, `getDouble()` 等。方法的参数是列名或列索引。

   ```java
   int id = resultSet.getInt("id");
   String name = resultSet.getString("name");
   ```

3. **检查列是否存在**：你可以使用 `ResultSet` 的 `findColumn()` 方法来检查某列是否存在。

   ```java
   int columnIndex = resultSet.findColumn("columnName");
   if (columnIndex > 0) {
       // 列存在
   } else {
       // 列不存在
   }
   ```

4. **获取结果集的元数据**：你可以使用 `ResultSet` 的 `getMetaData()` 方法来获取结果集的元数据，包括列数、列名等。

   ```java
   ResultSetMetaData metaData = resultSet.getMetaData();
   int columnCount = metaData.getColumnCount();
   String columnName = metaData.getColumnName(1);
   ```

5. **定位到特定行**：你可以使用 `ResultSet` 的 `absolute()` 方法将游标移动到结果集中的指定行。

   ```java
   resultSet.absolute(3); // 将游标移动到第 3 行
   ```

6. **关闭 `ResultSet`**：在使用完 `ResultSet` 后，务必调用 `close()` 方法来释放资源。

   ```java
   resultSet.close();
   ```

## 11.6 查询案例

```mysql
create database test;
use test;
CREATE TABLE user
(
    id int PRIMARY KEY,
    name varchar(50),
    age int,
    sex varchar(50)
);
alter table user change sex sex varchar(50) character set utf8;
INSERT INTO `user`(`id`, `name`, `age`, `sex`) VALUES (1, 'shi', 20, '男');
INSERT INTO `user`(`id`, `name`, `age`, `sex`) VALUES (2, 'yan', 13, '女');
INSERT INTO `user`(`id`, `name`, `age`, `sex`) VALUES (3, 'lou', 22, '女');
INSERT INTO `user`(`id`, `name`, `age`, `sex`) VALUES (4, 'admin', 50, '男');
```
- 查询 Id 为 1 的用户。
- 查询年龄为 13 岁，名字为 yan 的用户。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class JdbcTest {
    static final String DB_URL = "jdbc:mysql://localhost/test";
    static final String USER = "root";
    static final String PASS = "";

    public static void main(String[] args) {
        try {
            // 1. 创建数据库连接
            Connection connection = DriverManager.getConnection(DB_URL, USER, PASS);

            // 2. 执行第一个查询
            String sql1 = "SELECT name FROM user WHERE id >= 1";
            PreparedStatement preparedStatement1 = connection.prepareStatement(sql1);
            ResultSet resultSet1 = preparedStatement1.executeQuery();
            System.out.println("id >= 1");
            while (resultSet1.next()) {
                System.out.println(resultSet1.getString("name"));
            }

            // 3. 执行第二个查询
            String sql2 = "SELECT * FROM user WHERE age = 13 and name = 'yan'";
            PreparedStatement preparedStatement2 = connection.prepareStatement(sql2);
            ResultSet resultSet2 = preparedStatement2.executeQuery();
            System.out.println("find");
            while (resultSet2.next()) {
                System.out.println("name = " + resultSet2.getString("name"));
                System.out.println("sex = " + resultSet2.getString("sex"));
            }

            // 4. 关闭资源
            resultSet1.close();
            preparedStatement1.close();
            resultSet2.close();
            preparedStatement2.close();
            connection.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 11.7 事务管理

在 JDBC 中，你可以使用事务来管理数据库操作，以确保一组相关操作要么都成功提交，要么都回滚（撤销）。这是保证数据库操作的一致性和完整性的重要方式。

以下是在 JDBC 中进行事务管理的一般步骤：

1. **开启事务**：在执行 SQL 操作之前，你可以通过将自动提交（Auto-Commit）设置为 `false` 来开启事务。默认情况下，JDBC 是自动提交的，每个 SQL 语句都会立即生效。

   ```java
   connection.setAutoCommit(false); // 关闭自动提交
   ```

2. **执行数据库操作**：在事务中执行你的数据库操作，包括插入、更新、删除等。

   ```java
   // 执行数据库操作，例如 INSERT、UPDATE、DELETE
   ```

3. **提交事务**：如果所有的数据库操作都成功，你可以使用 `commit` 方法提交事务，使更改永久生效。

   ```java
   connection.commit(); // 提交事务
   ```

4. **回滚事务**：如果发生错误或某些操作失败，你可以使用 `rollback` 方法来回滚事务，使之前的更改不会生效。

   ```java
   connection.rollback(); // 回滚事务
   ```

5. **关闭连接**：最后，记得在完成事务后关闭数据库连接。

   ```java
   connection.close(); // 关闭数据库连接
   ```

下面是一个示例代码，演示了如何在 JDBC 中管理事务：

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class JdbcTransactionExample {
    public static void main(String[] args) {
        String jdbcUrl = "jdbc:mysql://localhost:3306/your_database";
        String username = "your_username";
        String password = "your_password";

        try (Connection connection = DriverManager.getConnection(jdbcUrl, username, password)) {
            connection.setAutoCommit(false); // 开启事务

            try {
                // 执行一些数据库操作
                Statement statement = connection.createStatement();
                statement.execute("INSERT INTO users (name, age) VALUES ('John', 30)");
                statement.execute("UPDATE users SET age = 31 WHERE name = 'John'");
                statement.execute("DELETE FROM users WHERE name = 'John'");

                connection.commit(); // 提交事务
                System.out.println("Transaction committed successfully.");
            } catch (SQLException e) {
                connection.rollback(); // 回滚事务
                System.err.println("Transaction rolled back due to an error: " + e.getMessage());
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

在这个示例中，我们首先将自动提交关闭，然后执行一系列数据库操作。如果操作都成功，我们提交事务。如果任何操作失败，我们回滚事务，以确保之前的更改不会生效。这样，你可以确保一组相关的操作要么全部成功，要么全部失败。

# 12 反射

在Java中，反射（Reflection）是一种强大的机制，允许程序在运行时检查、获取和操作类、对象、方法、字段等程序元素的信息，而不需要在编译时确定这些元素的类型。反射提供了一种途径，使你能够在运行时动态地获取和操作类的成员，而不必事先知道这些成员的名称或类型。这对于编写通用工具、框架和调试器非常有用。

在Java的反射机制中，有一些常用的类和接口，以下是其中一些主要的类和它们的用途：

1. **`java.lang.Class`**：`Class`类代表一个类的运行时类型信息。你可以使用它来获取类的各种信息，如类名、字段、方法、构造方法、父类、接口等。
2. **`java.lang.reflect.Field`**：`Field`类用于表示类中的字段（成员变量）。你可以使用它来获取和设置字段的值，包括私有字段。
3. **`java.lang.reflect.Method`**：`Method`类用于表示类中的方法。你可以使用它来调用类的方法，包括私有方法。
4. **`java.lang.reflect.Constructor`**：`Constructor`类用于表示类的构造方法。你可以使用它来实例化类的对象。
5. **`java.lang.reflect.Modifier`**：`Modifier`类包含了一组用于解析修饰符的静态方法，如`isPublic()`、`isStatic()`等。
6. **`java.lang.reflect.Array`**：`Array`类提供了创建和操作数组的静态方法，如`newInstance()`和`getLength()`。

使用这些类，你可以实现反射的各种功能。以下是使用反射的一般步骤：

1. 获取类的`Class`对象，通常使用`.class`关键字或`getClass()`方法。
2. 使用`Class`对象获取类的信息，如字段、方法或构造方法，通过`getFields()`, `getDeclaredFields()`, `getMethods()`, `getDeclaredMethods()`, `getConstructors()`, `getDeclaredConstructors()`等方法。
3. 创建类的对象，可以使用`Constructor`对象的`newInstance()`方法。
4. 操作字段和调用方法，使用`Field`对象的`get()`和`set()`方法，以及`Method`对象的`invoke()`方法。
5. 处理异常，因为反射可能引发`NoSuchMethodException`、`IllegalAccessException`等异常，需要适当捕获和处理。

```JAVA
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public void sayHello() {
        System.out.println("Hello, my name is " + name);
    }
}
```

```JAVA
import java.lang.reflect.*;

public class ReflectionExample {
    public static void main(String[] args) throws Exception {
        // 1. 获取类的Class对象
        Class<?> personClass = Class.forName("Person");

        // 2. 创建对象
        Constructor<?> constructor = personClass.getConstructor(String.class, int.class);
        Object person = constructor.newInstance("Alice", 30);

        // 3. 访问字段
        Field nameField = personClass.getDeclaredField("name");
        nameField.setAccessible(true);
        String name = (String) nameField.get(person);

        Field ageField = personClass.getDeclaredField("age");
        ageField.setAccessible(true);
        int age = (int) ageField.get(person);

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);

        // 4. 调用方法
        Method sayHelloMethod = personClass.getDeclaredMethod("sayHello");
        sayHelloMethod.setAccessible(true);
        sayHelloMethod.invoke(person);
    }
}

```

## 13 正则表达式

## 13.1 用法

1. 导入正则表达式的库：

```java
import java.util.regex.*;
```

1. 创建正则表达式模式对象（Pattern对象）：

```java
Pattern pattern = Pattern.compile("正则表达式");
```

1. 创建匹配器对象（Matcher对象）并使用模式匹配字符串：

```java
Matcher matcher = pattern.matcher("要匹配的字符串");
```

1. 使用匹配器对象进行匹配操作，并根据需要获取匹配结果：

```java
if (matcher.find()) {
    // 找到匹配
    String matchedText = matcher.group(); // 获取匹配的文本
    // 进行其他操作
} else {
    // 没有找到匹配
}
```

以下是一些常见的正则表达式用法示例：

- **查找匹配**：使用 `find()` 方法查找字符串中是否包含匹配正则表达式的部分。

```java
Pattern pattern = Pattern.compile("\\d+"); // 匹配一个或多个数字
Matcher matcher = pattern.matcher("12345 Hello 6789");
while (matcher.find()) {
    String matchedText = matcher.group();
    System.out.println("匹配到: " + matchedText);
}
```

- **替换**：使用 `replaceAll()` 方法将匹配的部分替换为指定的文本。

```java
String input = "Hello, World!";
String result = input.replaceAll("World", "Java");
System.out.println(result); // 输出: "Hello, Java!"
```

- **分割**：使用 `split()` 方法根据正则表达式分割字符串。

```java
String input = "apple,banana,grape";
String[] fruits = input.split(",");
for (String fruit : fruits) {
    System.out.println(fruit);
}
```
