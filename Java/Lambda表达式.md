# Lambda表达式

## Lambda表达式的标准格式

 Lambda表达式是JDK8开始后的一种新语法形式

```java
() -> {
    
}
```

- () 对应着方法的形参
- -> 固定格式
- {} 对应着方法的方法体

**注意点**:

- Lambda表达式可以用来简化匿名内部类的书写
- Lambda表达式只能简化函数式接口的匿名内部类的写法
- 函数式接口:
  - 有且仅有一个抽象方法的接口叫做函数式接口,接口上方可以加@FunctionalInterface注解

```java
package com.itheima.lambda;

import java.util.Arrays;

public class LambdaDemo1 {
    public static void main(String[] args) {
        //初识lambda表达式
        Integer[] arr = {2, 3, 1, 5, 5, 6, 7, 8, 4, 5};

        /*Arrays.sort(arr, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o1 - o2;
            }
        });*/

        Arrays.sort(arr, (Integer o1, Integer o2) -> {
                return o1 - o2;
            }
        );

        System.out.println(Arrays.toString(arr));//[1, 2, 3, 4, 5, 5, 5, 6, 7, 8]
    }
}

```

```java
package com.itheima.lambda;

public class LambdaDemo2 {
    public static void main(String[] args) {
        /*
        Lambda表达式的注意点:
            1.Lambda表达式可以用来简化匿名内部类的书写
            2.Lambda表达式只能简化函数式接口的匿名内部类的写法
            3.函数式接口:
                有且仅有一个抽象方法的接口叫做函数式接口,接口上方可以加@FunctionalInterface注解

         */

        //1.利用匿名内部类的形式去调用下面的方法
        //调用一个方法的时候,如果方法的形参是一个是一个接口,那么我们要传递这个接口的实现类对象
        //如果实现类对象只要用到一次,就可以用匿名内部类的形式进行书写

        method(new Swim() {
            @Override
            public void swimming() {
                System.out.println("正在游泳");
            }
        });

        //2.利用lambda表达式进行改写

        method(
                ()->{
                    System.out.println("正在游泳");
                }
        );



    }

    public static void method(Swim s){
        s.swimming();
    }
}


@FunctionalInterface
interface Swim{
    public abstract void swimming();
}

```

## Lambda表达式的省略写法

```java
package com.itheima.lambda;

import java.util.Arrays;

public class LambdaDemo3 {
    public static void main(String[] args) {
        /*
            lambda的省略规则:
                1.参数类型可以省略不写
                2.如果只有一个参数,参数类型可以省略,同时()也可以省略
                3.如果lambda表达式的方法体只有一行,大括号,分号,return可以省略不写,需要同时省略

         */

        Integer[] arr = {2, 3, 1, 5, 5, 6, 7, 8, 4, 5};

        /*Arrays.sort(arr, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o1 - o2;
            }
        });

        //lambda表达式完整格式
        Arrays.sort(arr, (Integer o1, Integer o2) -> {
                    return o1 - o2;
                }
        );*/

        //lambda表达式省略格式
        Arrays.sort(arr, (o1, o2) -> o1 - o2);

        System.out.println(Arrays.toString(arr));
    }
}

```

```java
package com.itheima.lambda;

import java.util.Arrays;

public class LambdaDemo4 {
    public static void main(String[] args) {
        /*
        定义数组并存储一些字符串,利用Arrays中的sort方法进行排序
        要求:
            按照字符串的长度进行排序,短的在前面,长的在后面
            (暂时不比较字符串里面的内容)
         */

        String[] arr = {"a", "aaaa", "aaa", "aa"};
        //a aa aaa aaaa

        //如果以后我们要把数组中的数据按照指定的方式进行排序,我们就需要用sort方法,而且要指定排序的规则
        /*Arrays.sort(arr, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return o1.length() - o2.length();
            }
        });*/

        //Lambda表达式完整格式
        /*Arrays.sort(arr, (String o1, String o2) -> {
                    return o1.length() - o2.length();
                }
        );*/

        //Lambda表达式省略格式
        //小括号:数据类型可以省略,如果参数只有一个,小括号还可以省略
        //大括号:如果方法体只有一行,return,分号,大括号都可以省略
        Arrays.sort(arr, (o1, o2) -> o1.length() - o2.length());

        //打印数组
        System.out.println(Arrays.toString(arr));
    }
}
```
