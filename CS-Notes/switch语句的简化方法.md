# 简介
---

这一小节用一个例子介绍一种简化switch语句的方法，当多个case的执行语句相同的时候可以使用。最后还用了一个JDK12的新特性，使得原本啰嗦不好看的代码变得非常简洁清晰。


# 例子
---

写一个程序，输入星期数，输出这一天是工作日或是休息日。星期一到星期五是工作日，星期六和星期日是休息日。

下面是一个比较啰嗦的写法：

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        System.out.println("输入一个星期数（1-7）");

        Scanner scanner = new Scanner(System.in);
        int number = scanner.nextInt();

        switch (number) {
            case 1:
                System.out.println("工作日");
                break;
            case 2:
                System.out.println("工作日");
                break;
            case 3:
                System.out.println("工作日");
                break;
            case 4:
                System.out.println("工作日");
                break;
            case 5:
                System.out.println("工作日");
                break;
            case 6:
                System.out.println("休息日");
                break;
            case 7:
                System.out.println("休息日");
                break;
            default:
                System.out.println("没有这个星期");
        }
    }
}
```


# 利用break穿透进行简化
---

如果case中不写break，程序将会继续往下执行而不是直接跳出switch，这成为break穿透。

下面是一个利用了break穿透的写法：

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        System.out.println("输入一个星期数（1-7）");

        Scanner scanner = new Scanner(System.in);
        int number = scanner.nextInt();

        switch (number) {
            case 1:
            case 2:
            case 3:
            case 4:
            case 5:
                System.out.println("工作日");
                break;
            case 6:
            case 7:
                System.out.println("休息日");
                break;
            default:
                System.out.println("没有这个星期");
        }
    }
}
```


# 使用case合并继续简化
---

这里用了一个相对不为人知的知识点：case后面可以写多个值。

下面是一个用了case合并的写法：

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        System.out.println("输入一个星期数（1-7）");

        Scanner scanner = new Scanner(System.in);
        int number = scanner.nextInt();

        switch (number) {
            case 1, 2, 3, 4, 5:
                System.out.println("工作日");
                break;
            case 6, 7:
                System.out.println("休息日");
                break;
            default:
                System.out.println("没有这个星期");
        }
    }
}
```


# 使用新写法继续简化
---

[[switch语句的新写法]]

下面是一个用了JDK12新特性的写法：

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        System.out.println("输入一个星期数（1-7）");

        Scanner scanner = new Scanner(System.in);
        int number = scanner.nextInt();

        switch (number) {
            case 1, 2, 3, 4, 5 -> System.out.println("工作日");
            case 6, 7 -> System.out.println("休息日");
            default -> System.out.println("没有这个星期");
        }
    }
}
```


# 未完待续
---

甚至可以用switch的返回值进一步简化代码，不过等下次再补充吧。