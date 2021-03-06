# Equals和==的区别


[Equals和==的区别](https://www.jianshu.com/p/9cbed9f33a4d)
<!--more-->


常常会用equals和==判断两个对象是否相等，那么两者有什么不同呢？主要有以下几点区别

- 首先区别的是 equals 是方法，但是 == 是操作符
- 对于基本类型的变量(int, short, long, float, double), 只能用==去比较，一般比较的就是他们的value
- 对于引用类型的变量来说，例如String类型，就是String继承了Object类， equals是Object类的通用方法，对于该类型对象的比较，默认情况下，也就是没有复写 Object 类的 equals 方法，使用 == 和 equals 比较是一样效果的，都是比较的是它们在内存中的存放地址。
- 但是对于某些类来说，为了满足自身业务需求，可能存在 equals 方法被复写的情况，这时使用 equals 方法比较需要看具体的情况，例如 String 类，使用 equals 方法会比较它们的值；|| 区别就看有没有重写这个equals method

```java
    String a = "Hello World";
    String b = new String("Hello World");
    String c = b; //引用传递
    System.out.println("a == b:" + a == b);             //false
    System.out.println("b == c:" + b == c);             //true
    System.out.println("a == c:" + a == c);             //false
    System.out.println("a.equals(b):" + a.equals(b));   //true
    System.out.println("b.equals(c):" + b.equals(c));   //true
    System.out.println("a.equals(c):" + a.equals(c));   //true

    /*
    最终的打印会是：
    a == b:false
    b == c:true
    a == c:false
    a.equals(b):true
    b.equals(c):true
    a.equals(c):true
    */
```


因为 String b 通过 new 的方式已经开辟了新的堆内存，而 String a = "Hello World" 是存放在常量池里的，两者在 Java 内存里存在放的位置是不同的，所以 a == b 为 false；而 equals 方法当两者存放的内存地址不同时，会比较两者的值，两者的值都是 "Hello World" ，所以 a.equals(b) 为 true。
