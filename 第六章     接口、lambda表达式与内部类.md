#                 第六章     接口、lambda表达式与内部类

### 6.1接口

在java中，接口不是类，而是对希望符合这个接口的类的一组需求，所以不能用new。

在接口中所有方法都是public，可以不用写修饰符，但是，实现类在实现接口时，必须将方法声明为public。

尽管不能构造接口，但可以声明一个接口。

接口也可以继承，以此来扩展接口。

接口中的方法自动为public，字段自动为public static final;

![Screenshot_20240118_131157_Samsung Notes](C:\Users\21905\Downloads/Screenshot_20240118_131157_Samsung Notes.jpg)

![Screenshot_20240118_131105_Samsung Notes](C:\Users\21905\Downloads/Screenshot_20240118_131105_Samsung Notes.jpg)

默认的克隆操作为浅拷贝

即使clone的默认（浅拷贝）实现能够满足要求，还是需要实现Cloneable接口，将clone重新定义为public。

![Screenshot_20240118_132308_Samsung Notes](C:\Users\21905\Downloads/Screenshot_20240118_132308_Samsung Notes.jpg)

也就是说，还得调用那些可变字段的克隆函数。

Cloneable接口是标记接口，不含有任何方法，唯一作用就是允许在类型查询中使用instanceof。这个接口只是作为一个标记，指示类设计者了解克隆过程。如果一个类没有实现cloneable接口，但是使用了clone方法，就会抛出异常。

### 6.2   lambda表达式

**表达式结构**：(参数列表) -> { 表达式或语句块 }

**参数列表**：这与定义方法时的参数列表类似。它可以是空的，或者包含一个或多个参数。参数类型可以明确声明，也可以让Java编译器通过上下文推断（类型推断）。

**箭头符号** `->`：这个符号是lambda表达式的关键，它将参数列表和表达式或代码块分开。

**表达式或语句块**：这是lambda表达式的主体，可以是单个表达式或一个更复杂的代码块。对于单个表达式，花括号可以省略；对于代码块，需要用花括号括起来。

实例：

( ) -> System.out.println("Hello World");

s -> s.length( );

(int a, int b) -> a + b;

(String s) -> {
    System.out.println(s);
    return s.length();
};

Lambda表达式主要用于提供一种简洁的方式来实现只有一个抽象方法的接口（函数式接口），如 `Runnable`、`Callable`、`Comparator` 等。它们使代码变得更加简洁、清晰，尤其是在使用函数式编程风格的时候。

## 6.3   内部类

使用内部类的原因：

- 内部类可以对同一个包中的其他类隐藏。
- 内部类方法可以访问定义这些方法的作用域中的数据，包括原本私有的数据。

内部类对象总有一个隐式引用，指向创建它的外部类对象。

![Screenshot_20240118_143520_Samsung Notes](C:\Users\21905\Downloads\Screenshot_20240118_143520_Samsung Notes.jpg)

### 局部内部类

声明局部类时不能有访问说明符。局部类的作用域总是限定在声明局部类的块中。

**成员内部类（非静态内部类）**：

- 定义在另一个类的内部，与实例方法和变量同级。
- 可以访问外部类的所有成员，包括私有成员。
- 需要外部类的实例来创建对象。
- 不能有静态数据成员和静态方法。

代码：public class OuterClass {
    private int num = 10;

    class InnerClass {
        public void display() {
            System.out.println("num: " + num);
        }
    }
    }
**静态内部类**：

- 也是定义在另一个类内部，但是使用 `static` 修饰。
- 可以访问外部类的静态成员，但不能直接访问非静态成员。
- 可以有自己的静态成员。
- 可以不依赖外部类的实例而独立存在。

代码：public class OuterClass {
    private static int num = 10;

    static class StaticInnerClass {
        public void display() {
            System.out.println("num: " + num);
        }
    }
}

**局部内部类**：

- 定义在一个方法或作用域内。
- 只在定义它的方法或作用域内可见和可用。
- 可以访问外部类的所有成员以及final或effectively final的局部变量。

代码：public class OuterClass {
    public void someMethod() {
        class LocalInnerClass {
            public void display() {
                System.out.println("Inside local inner class.");
            }
        }
    }
}

**匿名内部类**：

- 没有名称的内部类。
- 通常用于实现接口或扩展类的实例。
- 用于创建一次性使用的类实例。
- 适用于回调和事件监听等场景。

常与lambda表达式一起使用。



局部内部类和匿名内部类都是定义在方法内部等局部，匿名内部类通常用于实现接口和继承类。