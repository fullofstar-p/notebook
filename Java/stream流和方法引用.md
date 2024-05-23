## 1.不可变集合

### 1.1 什么是不可变集合

​	是一个长度不可变，内容也无法修改的集合

### 1.2 使用场景

​	如果某个数据不能被修改，把它防御性地拷贝到不可变集合中是个很好的实践。

​	当集合对象被不可信的库调用时，不可变形式是安全的。

简单理解：

​	不想让别人修改集合中的内容

比如说：

1，斗地主的54张牌，是不能添加，不能删除，不能修改的

2，斗地主的打牌规则：单张，对子，三张，顺子等，也是不能修改的

3，用代码获取的操作系统硬件信息，也是不能被修改的

| 方法名称                                | 说明                               |
| --------------------------------------- | ---------------------------------- |
| static<E> List<E> of(E...elements)      | 创建一个具有指定元素的List集合对象 |
| static<E> Set<E> of(E...elements)       | 创建一个具有指定元素的Set集合对象  |
| static<K,V>  Map<K,V>  of(E...elements) | 创建一个具有指定元素的Map集合对象  |

==**注意**==:这个集合不能添加,删除,修改

### 1.3 不可变集合分类

* 不可变的list集合
* 不可变的set集合
* 不可变的map集合

### 1.4 不可变的list集合

```java
public class ImmutableDemo1 {
    public static void main(String[] args) {
        /*
            创建不可变的List集合
            "张三", "李四", "王五", "赵六"
        */

        //一旦创建完毕之后，是无法进行修改的，在下面的代码中，只能进行查询操作
        List<String> list = List.of("张三", "李四", "王五", "赵六");

        System.out.println(list.get(0));
        System.out.println(list.get(1));
        System.out.println(list.get(2));
        System.out.println(list.get(3));

        System.out.println("---------------------------");

        for (String s : list) {
            System.out.println(s);
        }

        System.out.println("---------------------------");


        Iterator<String> it = list.iterator();
        while(it.hasNext()){
            String s = it.next();
            System.out.println(s);
        }
        System.out.println("---------------------------");

        for (int i = 0; i < list.size(); i++) {
            String s = list.get(i);
            System.out.println(s);
        }
        System.out.println("---------------------------");

        //list.remove("李四");
        //list.add("aaa");
        list.set(0,"aaa");
    }
}
```

### 1.5 不可变的Set集合

```java
public class ImmutableDemo2 {
    public static void main(String[] args) {
        /*
           创建不可变的Set集合
           "张三", "李四", "王五", "赵六"


           细节：
                当我们要获取一个不可变的Set集合时，里面的参数一定要保证唯一性
        */

        //一旦创建完毕之后，是无法进行修改的，在下面的代码中，只能进行查询操作
        Set<String> set = Set.of("张三", "张三", "李四", "王五", "赵六");

        for (String s : set) {
            System.out.println(s);
        }

        System.out.println("-----------------------");

        Iterator<String> it = set.iterator();
        while(it.hasNext()){
            String s = it.next();
            System.out.println(s);
        }

        System.out.println("-----------------------");
        //set.remove("王五");
    }
}
```

### 1.6 不可变的Map集合

#### 1.6.1：键值对个数小于等于10

```java
public class ImmutableDemo3 {
    public static void main(String[] args) {
       /*
        创建Map的不可变集合
            细节1：
                键是不能重复的
            细节2：
                Map里面的of方法，参数是有上限的，最多只能传递20个参数，10个键值对
            细节3：
                如果我们要传递多个键值对对象，数量大于10个，在Map接口中还有一个方法
        */

        //一旦创建完毕之后，是无法进行修改的，在下面的代码中，只能进行查询操作
        Map<String, String> map = Map.of("张三", "南京", "张三", "北京", "王五", "上海",
                "赵六", "广州", "孙七", "深圳", "周八", "杭州",
                "吴九", "宁波", "郑十", "苏州", "刘一", "无锡",
                "陈二", "嘉兴");

        Set<String> keys = map.keySet();
        for (String key : keys) {
            String value = map.get(key);
            System.out.println(key + "=" + value);
        }

        System.out.println("--------------------------");

        Set<Map.Entry<String, String>> entries = map.entrySet();
        for (Map.Entry<String, String> entry : entries) {
            String key = entry.getKey();
            String value = entry.getValue();
            System.out.println(key + "=" + value);
        }
        System.out.println("--------------------------");
    }
}
```

#### 1.6.2：键值对个数大于10

```java
package com.itheima.immutable;

import java.util.HashMap;
import java.util.Map;

public class ImmutableDemo4 {
    public static void main(String[] args) {
        /*
        创建Map的不可变集合,键值对的数量超过10个
         */

        //1.创建一个普通的Map集合
        HashMap<String, String> hm = new HashMap<>();hm.put("张三","南京");
        hm.put("李四","北京");
        hm.put("王五","上海");
        hm.put("赵六","北京");
        hm.put("孙七","深圳");
        hm.put("周八","杭州");
        hm.put("吴九","宁波");
        hm.put("郑十","苏州");
        hm.put("刘一","无锡");
        hm.put("陈二","嘉兴");
        hm.put("aaa","111");

        //2.利用上面的数据来获取一个不可变的集合
       /* //获取到所有的键值对对象 (Entry对象)
        Set<Map.Entry<String, String>> entries = hm.entrySet();
        //把entries变成一个数组
        //Map.Entry[] arr = entries.toArray(new Map.Entry[0]);

       *//* Object[] objects = entries.toArray();
        for (Object object : objects) {
            System.out.println(object);
        }*//*

        Map.Entry[] arr1 = new Map.Entry[0];
        //toArray方法在底层会比较集合的长度跟数组的长度两者的大小
        //如果集合的长度 > 数组的长度 : 数据在数组中放不下,此时会根据实际数据的个数,重新创建数组
        //如果集合的长度 <= 数组的长度 : 数据在数组中放的下,此时不会创建新的数组,而是直接用
        Map.Entry[] arr2 = entries.toArray(arr1);

        //不可变得map集合
        Map map = Map.ofEntries(arr2);

        //map.put("bbb","222");*/

        //Map<Object, Object> map = Map.ofEntries(hm.entrySet().toArray(new Map.Entry[0]));
        
        //Map.copyOf jdk10出现
        Map<String, String> map = Map.copyOf(hm);
        //map.put("bbb","222");

    }
}

```

## 2.Stream流

### 2.1体验Stream流【理解】

- 案例需求

  按照下面的要求完成集合的创建和遍历

  - 创建一个集合，存储多个字符串元素
  - 把集合中所有以"张"开头的元素存储到一个新的集合
  - 把"张"开头的集合中的长度为3的元素存储到一个新的集合
  - 遍历上一步得到的集合

- 原始方式示例代码

  ```java
  public class MyStream1 {
      public static void main(String[] args) {
          //集合的批量添加
          ArrayList<String> list1 = new ArrayList<>(List.of("张三丰","张无忌","张翠山","王二麻子","张良","谢广坤"));
          //list.add()

          //遍历list1把以张开头的元素添加到list2中。
          ArrayList<String> list2 = new ArrayList<>();
          for (String s : list1) {
              if(s.startsWith("张")){
                  list2.add(s);
              }
          }
          //遍历list2集合，把其中长度为3的元素，再添加到list3中。
          ArrayList<String> list3 = new ArrayList<>();
          for (String s : list2) {
              if(s.length() == 3){
                  list3.add(s);
              }
          }
          for (String s : list3) {
              System.out.println(s);
          }      
      }
  }
  ```

- 使用Stream流示例代码

  ```java
  public class StreamDemo {
      public static void main(String[] args) {
          //集合的批量添加
          ArrayList<String> list1 = new ArrayList<>(List.of("张三丰","张无忌","张翠山","王二麻子","张良","谢广坤"));

          //Stream流
          list1.stream().filter(s->s.startsWith("张"))
                  .filter(s->s.length() == 3)
                  .forEach(s-> System.out.println(s));
      }
  }
  ```

- Stream流的好处

  - 直接阅读代码的字面意思即可完美展示无关逻辑方式的语义：获取流、过滤姓张、过滤长度为3、逐一打印
  - Stream流把真正的函数式编程风格引入到Java中
  - 代码简洁

### 2.2Stream流的常见生成方式【应用】

- Stream流的思想

  ![01_Stream流思想](.\img\01_Stream流思想.png)

- Stream流的三类方法

  - 获取Stream流
    - 创建一条流水线,并把数据放到流水线上准备进行操作
  - 中间方法
    - 流水线上的操作
    - 一次操作完毕之后,还可以继续进行其他操作
  - 终结方法
    - 一个Stream流只能有一个终结方法
    - 是流水线上的最后一个操作

- 生成Stream流的方式

  - Collection体系集合

    使用默认方法stream()生成流， default Stream<E> stream()

  - Map体系集合

    把Map转成Set集合，间接的生成流

  - 数组

    通过Arrays中的静态方法stream生成流

  - 同种数据类型的多个数据

    通过Stream接口的静态方法of(T... values)生成流

- | 获取方式     | 方法名                                       | 说明                                                         |
  | ------------ | -------------------------------------------- | ------------------------------------------------------------ |
  | 单列集合     | default Stream<E> Stream()                   | Collection中的默认方法                                       |
  | 双列集合     | 无                                           | 无法直接使用Stream流(==需要先通过keySet()或entrySet()转成单列集合再获取Stream流==) |
  | 数组         | public static<T> Stream<T> stream(T[] array) | Arrays工具类中的静态方法                                     |
  | 一些零散数据 | public static<T> Stream<T> of(T...values)    | Stream接口中的静态方法                                       |

- 代码演示

  ```java
  public class StreamDemo {
      public static void main(String[] args) {
          //Collection体系的集合可以使用默认方法stream()生成流
          List<String> list = new ArrayList<String>();
          Stream<String> listStream = list.stream();
  
          Set<String> set = new HashSet<String>();
          Stream<String> setStream = set.stream();
  
          //Map体系的集合间接的生成流
          Map<String,Integer> map = new HashMap<String, Integer>();
          Stream<String> keyStream = map.keySet().stream();
          Stream<Integer> valueStream = map.values().stream();
          Stream<Map.Entry<String, Integer>> entryStream = map.entrySet().stream();
  
          //数组可以通过Arrays中的静态方法stream生成流
          String[] strArray = {"hello","world","java"};
          Stream<String> strArrayStream = Arrays.stream(strArray);
        
        	//同种数据类型的多个数据可以通过Stream接口的静态方法of(T... values)生成流
          //注意:
          //stream接口中静态方法of的细节
          //方法的形参是一个可变参数,可以传递一堆零散数据,也可以传递数组,但是数组必须是引用数据类型的,是会把整个数组当作一个元素,放到stream当中.
          Stream<String> strArrayStream2 = Stream.of("hello", "world", "java");
          Stream<Integer> intStream = Stream.of(10, 20, 30);
      }
  }
  ```

### 2.3Stream流中间操作方法【应用】

- 概念

  中间操作的意思是,执行完此方法之后,Stream流依然可以继续执行其他操作

- 常见方法

  | 方法名                                          | 说明                                                       |
  | ----------------------------------------------- | ---------------------------------------------------------- |
  | Stream<T> filter(Predicate predicate)           | 用于对流中的数据进行过滤                                   |
  | Stream<T> limit(long maxSize)                   | 返回此流中的元素组成的流，截取前指定参数个数的数据         |
  | Stream<T> skip(long n)                          | 跳过指定参数个数的数据，返回由该流的剩余元素组成的流       |
  | static <T> Stream<T> concat(Stream a, Stream b) | 合并a和b两个流为一个流                                     |
  | Stream<T> distinct()                            | 返回由该流的不同元素（根据Object.equals(Object) ）组成的流 |
  | map                                             | 转换流中的数据类型                                         |

  ==注意1==:中间方法,返回新的stream流,原来的stream流只能使用一次,建议使用链式编程

  ==注意2==:修改stream流中的数据,不会影响原来集合或者数组中的数据

- filter代码演示

  ```java
  public class MyStream3 {
      public static void main(String[] args) {
  //        Stream<T> filter(Predicate predicate)：过滤
  //        Predicate接口中的方法	boolean test(T t)：对给定的参数进行判断，返回一个布尔值

          ArrayList<String> list = new ArrayList<>();
          list.add("张三丰");
          list.add("张无忌");
          list.add("张翠山");
          list.add("王二麻子");
          list.add("张良");
          list.add("谢广坤");

          //filter方法获取流中的 每一个数据.
          //而test方法中的s,就依次表示流中的每一个数据.
          //我们只要在test方法中对s进行判断就可以了.
          //如果判断的结果为true,则当前的数据留下
          //如果判断的结果为false,则当前数据就不要.
  //        list.stream().filter(
  //                new Predicate<String>() {
  //                    @Override
  //                    public boolean test(String s) {
  //                        boolean result = s.startsWith("张");
  //                        return result;
  //                    }
  //                }
  //        ).forEach(s-> System.out.println(s));

          //因为Predicate接口中只有一个抽象方法test
          //所以我们可以使用lambda表达式来简化
  //        list.stream().filter(
  //                (String s)->{
  //                    boolean result = s.startsWith("张");
  //                        return result;
  //                }
  //        ).forEach(s-> System.out.println(s));

          list.stream().filter(s ->s.startsWith("张")).forEach(s-> System.out.println(s));

      }
  }
  ```

- limit&skip代码演示

  ```java
  public class StreamDemo02 {
      public static void main(String[] args) {
          //创建一个集合，存储多个字符串元素
          ArrayList<String> list = new ArrayList<String>();

          list.add("林青霞");
          list.add("张曼玉");
          list.add("王祖贤");
          list.add("柳岩");
          list.add("张敏");
          list.add("张无忌");

          //需求1：取前3个数据在控制台输出
          list.stream().limit(3).forEach(s-> System.out.println(s));
          System.out.println("--------");

          //需求2：跳过3个元素，把剩下的元素在控制台输出
          list.stream().skip(3).forEach(s-> System.out.println(s));
          System.out.println("--------");

          //需求3：跳过2个元素，把剩下的元素中前2个在控制台输出
          list.stream().skip(2).limit(2).forEach(s-> System.out.println(s));
      }
  }
  ```

- concat&distinct代码演示

  ```java
  public class StreamDemo03 {
      public static void main(String[] args) {
          //创建一个集合，存储多个字符串元素
          ArrayList<String> list = new ArrayList<String>();
  
          list.add("林青霞");
          list.add("张曼玉");
          list.add("王祖贤");
          list.add("柳岩");
          list.add("张敏");
          list.add("张无忌");
  
          //需求1：取前4个数据组成一个流
          Stream<String> s1 = list.stream().limit(4);
  
          //需求2：跳过2个数据组成一个流
          Stream<String> s2 = list.stream().skip(2);
  
          //需求3：合并需求1和需求2得到的流，并把结果在控制台输出
  //        Stream.concat(s1,s2).forEach(s-> System.out.println(s));
  
          //需求4：合并需求1和需求2得到的流，并把结果在控制台输出，要求字符串元素不能重复
          Stream.concat(s1,s2).distinct().forEach(s-> System.out.println(s));
      }
  }
  ```

- map代码演示

  ```java
  package com.itheima.stream;
  
  import java.util.ArrayList;
  import java.util.Collections;
  
  public class StreamDemo8 {
      public static void main(String[] args) {
          /*
              map             转换流中的数据类型
  
              注意1：中间方法，返回新的Stream流，原来的Stream流只能使用一次，建议使用链式编程
              注意2：修改Stream流中的数据，不会影响原来集合或者数组中的数据
           */
  
          ArrayList<String> list= new ArrayList<>();
          Collections.addAll(list,"张无忌-15","周芷若-14","赵敏-13","张强-20","张三丰-100","张翠山-40","张良-35","王二麻子-37","谢广坤-41");
  
          //需求:只获取里面的年龄并进行打印
          //String -> int
  
          //第一个类型:流中原本的数据类型
          //第二个类型:要转成之后的类型
  
          //apply的形参s:依次表示流里面的每一个数据
          //返回值:表示转换之后的数据
  
          //当map方法执行完毕之后,流上的数据就变成了整数
          //所以在下面forEach当中,s依次表示流里面的每一个数据,这个数据现在就是整数了
          /*list.stream().map(new Function<String, Integer>() {
              @Override
              public Integer apply(String s) {
                  String[] arr = s.split("-");
                  String ageString  = arr[1];
                  int age = Integer.parseInt(ageString);
                  return age;
              }
          }).forEach(s -> System.out.println(s));*/
  
          //"张无忌-15"
          list.stream()
                  .map(s -> Integer.parseInt(s.split("-")[1]))
                  .forEach(s -> System.out.println(s));
      }
  }
  
  ```

### 2.4Stream流终结操作方法【应用】

- 概念

  终结操作的意思是,执行完此方法之后,Stream流将不能再执行其他操作

- 常见方法

  | 方法名                        | 说明                      |
  | ----------------------------- | ------------------------- |
  | void forEach(Consumer action) | 对此流的每个元素执行操作  |
  | long count()                  | 返回此流中的元素数        |
  | toArray()                     | 收集流中的数据,放到数组中 |
  | collect(Collector collector)  | 收集流中的数据,放到集合中 |

- 代码演示

  ```java
  package com.itheima.stream;
  
  import java.util.ArrayList;
  import java.util.Arrays;
  import java.util.Collections;
  
  public class StreamDemo9 {
      public static void main(String[] args) {
          /*
              void forEach(Consumer action)       遍历
              long count()                        统计
              toArray()                           收集流中的数据，放到数组中
  
           */
  
          ArrayList<String> list = new ArrayList<>();
          Collections.addAll(list, "张无忌","周芷若","赵敏","张强","张三丰","张翠山","张良","王二麻子","谢广坤");
  
          //void forEach(Consumer action)       遍历
  
          //Consumer的泛型:表示流中数据的类型
          //accept方法的形参s:依次表示流里面的每一个数据
          //方法体:对每一个数据的处理操作(打印)
          /*list.stream().forEach(new Consumer<String>() {
              @Override
              public void accept(String s) {
                  System.out.println(s);
              }
          });*/
          //list.stream().forEach(s -> System.out.println(s));
  
          // long count()                        统计
         /* long count = list.stream().count();
          System.out.println(count);*/
  
          // toArray()                           收集流中的数据，放到数组中
         /* Object[] arr1 = list.stream().toArray();
          System.out.println(Arrays.toString(arr1));*/
  
  
          //IntFunction的泛型: 具体类型的数组
          //apply的形参:流中数据的个数,要跟数组的长度保持一致
          //apply的返回值:具体类型的数组
          //方法体:就是创建数组
  
          //toArray方法的参数的作用,负责创建一个指定类型的数组
          //toArray方法的底层,会依次得到流里面的每一个数据,并把数据放到数组当中
          //toArray方法的返回值,是一个装着流里面所有数据的数组
         /* String[] arr = list.stream().toArray(new IntFunction<String[]>() {
              @Override
              public String[] apply(int value) {
                  return new String[value];
              }
          });
          System.out.println(Arrays.toString(arr));*/
  
          String[] arr2 = list.stream().toArray(value -> new String[value]);
          System.out.println(Arrays.toString(arr2));
  
  
      }
  }
  
  ```

### 2.5Stream流的收集操作【应用】

- 概念

  对数据使用Stream流的方式操作完毕后,可以把流中的数据收集到集合中

- 常用方法

  | 方法名                            | 说明        |
  | ------------------------------ | --------- |
  | R collect(Collector collector) | 把结果收集到集合中 |

- 工具类Collectors提供了具体的收集方式

  | 方法名                                                       | 说明                   |
  | ------------------------------------------------------------ | ---------------------- |
  | public static <T> Collector toList()                         | 把元素收集到List集合中 |
  | public static <T> Collector toSet()                          | 把元素收集到Set集合中  |
  | public static  Collector toMap(Function keyMapper,Function valueMapper) | 把元素收集到Map集合中  |

- 代码演示

  ```java
  package com.itheima.stream;
  
  import java.util.*;
  import java.util.function.Function;
  import java.util.stream.Collectors;
  
  public class StreamDemo10 {
      public static void main(String[] args) {
          /*
          collect(Collector collector)              收集流中的数据,放到集合中(List Set Map)
          注意点:
              如果我们要收集到Map集合中,键不能重复,否则会报错
           */
  
          ArrayList<String> list = new ArrayList<>();
          Collections.addAll(list, "张无忌-男-15", "周芷若-女-14", "赵敏-女-13", "张强-男-20", "张三丰-男-100", "张翠山-男-40", "张良-男-35", "王二麻子-男-37", "谢广坤-男-41");
  
          //收集到List集合当中
          //需求:
          //我要把所有的男性收集起来
          List<String> newList1 = list.stream().filter(s -> "男".equals(s.split("-")[1])).collect(Collectors.toList());
          //System.out.println(newList1);
  
          //收集到Set集合当中
          //需求:
          //我要把所有的男性收集起来
          Set<String> newList2 = list.stream().filter(s -> "男".equals(s.split("-")[1])).collect(Collectors.toSet());
          //System.out.println(newList2);
  
          //收集到Map集合当中
          //需求:
          //我要把所有的男性收集起来
          //谁作为键,谁作为值
          //键:姓名  值:年龄
          Map<String, Integer> map = list.stream()
                  .filter(s -> "男".equals(s.split("-")[1])).collect(Collectors.toMap(new Function<String, String>() {
                      /*
                          toMap:  参数一:表示键的生成规则
                                  参数二:表示值的生成规则
  
                          参数一:
                                  Function泛型一:表示流中的每一个数据类型
                                          泛型二:表示Map集合中键的数据类型
  
                                  方法apply形参:依次表示流里面的每一个数据
                                          方法体:生成键的代码
                                          返回值:已经生成的键
  
                          参数二:
                                  Function泛型一:表示流中的每一个数据类型
                                          泛型二:表示Map集合中值的数据类型
  
                                  方法apply形参:依次表示流里面的每一个数据
                                          方法体:生成值的代码
                                          返回值:已经生成的值
  
                       */
                      @Override
                      public String apply(String s) {
                          return s.split("-")[0];
                      }
                  }, new Function<String, Integer>() {
                      @Override
                      public Integer apply(String s) {
                          return Integer.parseInt(s.split("-")[2]);
                      }
                  }));
  
          //System.out.println(map);
  
          Map<String, Integer> map2 = list.stream()
                  .filter(s -> "男".equals(s.split("-")[1]))
                  .collect(Collectors.toMap(s -> s.split("-")[0], s -> Integer.parseInt(s.split("-")[2])));
  
          //System.out.println(map2);
  
  
  
  
      }
  }
  ```

### 2.6Stream流综合练习【应用】

- 案例需求

  现在有两个ArrayList集合，分别存储6名男演员名称和6名女演员名称，要求完成如下的操作

  - 男演员只要名字为3个字的前三人
  - 女演员只要姓林的，并且不要第一个
  - 把过滤后的男演员姓名和女演员姓名合并到一起
  - 把上一步操作后的元素作为构造方法的参数创建演员对象,遍历数据

  演员类Actor已经提供，里面有一个成员变量，一个带参构造方法，以及成员变量对应的get/set方法

- 代码实现

  演员类
  ```java
  public class Actor {
      private String name;
  
      public Actor(String name) {
          this.name = name;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  }
  ```

  测试类

  ```java
  public class StreamTest {
      public static void main(String[] args) {
          //创建集合
          ArrayList<String> manList = new ArrayList<String>();
          manList.add("周润发");
          manList.add("成龙");
          manList.add("刘德华");
          manList.add("吴京");
          manList.add("周星驰");
          manList.add("李连杰");
    
          ArrayList<String> womanList = new ArrayList<String>();
          womanList.add("林心如");
          womanList.add("张曼玉");
          womanList.add("林青霞");
          womanList.add("柳岩");
          womanList.add("林志玲");
          womanList.add("王祖贤");
    
          //男演员只要名字为3个字的前三人
          Stream<String> manStream = manList.stream().filter(s -> s.length() == 3).limit(3);
    
          //女演员只要姓林的，并且不要第一个
          Stream<String> womanStream = womanList.stream().filter(s -> s.startsWith("林")).skip(1);
    
          //把过滤后的男演员姓名和女演员姓名合并到一起
          Stream<String> stream = Stream.concat(manStream, womanStream);
    
        	// 将流中的数据封装成Actor对象之后打印
        	stream.forEach(name -> {
              Actor actor = new Actor(name);
              System.out.println(actor);
          }); 
      }
  }
  ```

```java
package com.itheima.test;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.stream.Collectors;

public class Test1 {
    public static void main(String[] args) {
        /*
            定义一个集合，并添加一些整数1,2,3,4,5,6,7,8,9,10
            过滤奇数，只留下偶数。
            并将结果保存起来
         */
        //1.定义一个集合
        ArrayList<Integer> list = new ArrayList<>();
        //2.添加元素
        Collections.addAll(list,1,2,3,4,5,6,7,8,9,10);
        //3.过滤奇数，只留下偶数
        //进行判断,如果是偶数,返回true 保留
        List<Integer> newList = list.stream()
                .filter(s -> s % 2 == 0)
                .collect(Collectors.toList());
        //4.打印集合
        System.out.println(newList);

    }
}
```



## 3.方法引用

### 3.1体验方法引用【理解】

- 方法引用的出现原因

  在使用Lambda表达式的时候，我们实际上传递进去的代码就是一种解决方案：拿参数做操作

  那么考虑一种情况：如果我们在Lambda中所指定的操作方案，已经有地方存在相同方案，那是否还有必要再写重复逻辑呢？答案肯定是没有必要

  那我们又是如何使用已经存在的方案的呢？

  这就是我们要讲解的方法引用，我们是通过方法引用来使用已经存在的方案

- 代码演示

  ```java
  public interface Printable {
      void printString(String s);
  }
  
  public class PrintableDemo {
      public static void main(String[] args) {
          //在主方法中调用usePrintable方法
  //        usePrintable((String s) -> {
  //            System.out.println(s);
  //        });
  	    //Lambda简化写法
          usePrintable(s -> System.out.println(s));
  
          //方法引用
          usePrintable(System.out::println);
  
      }
  
      private static void usePrintable(Printable p) {
          p.printString("爱生活爱Java");
      }
  }
  
  ```

```java
package com.itheima.function;

import java.util.Arrays;

public class FunctionDemo1 {
    public static void main(String[] args) {
        //需求:创建一个数组,进行倒序排列
        Integer[] arr = {3, 5, 4, 1, 6, 2};
        //匿名内部类
        /*Arrays.sort(arr, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2 - o1;
            }
        });*/
        //System.out.println(Arrays.toString(arr));

        //Lambda表达式
        //因为第二个参数的类型Comparator是一个函数式接口
       /* Arrays.sort(arr, (Integer o1, Integer o2) -> {
            return o2 - o1;
        });*/

        //System.out.println(Arrays.toString(arr));

        //Lambda表达式简化格式
        //Arrays.sort(arr, (o1, o2) -> o2 - o1);
        //System.out.println(Arrays.toString(arr));

        //方法引用
        //1.引用处需要是函数式接口
        //2.被引用的方法需要已经存在
        //3.被引用方法的形参和返回值需要和抽象方法的形参和返回值保持一致
        //4.被引用方法的功能需要满足当前的需求

        //表示引用FunctionDemo1类里面的的subtraction方法
        //把这个方法当作抽象方法的方法体
        Arrays.sort(arr,FunctionDemo1::subtraction);

        System.out.println(Arrays.toString(arr));
    }

    //可以是Java已经写好的,也可以是一些第三方的工具类
    public static int subtraction(int num1, int num2) {
        return num2 - num1;
    }
}
```



### 3.2方法引用符【理解】

- 方法引用符

  `::`  该符号为引用运算符，而它所在的表达式被称为方法引用

- 推导与省略

  - 如果使用Lambda，那么根据“可推导就是可省略”的原则，无需指定参数类型，也无需指定的重载形式，它们都将被自动推导
  - 如果使用方法引用，也是同样可以根据上下文进行推导
  - 方法引用是Lambda的孪生兄弟

### 3.3引用类方法(引用静态方法)【应用】

​	引用类方法，其实就是引用类的静态方法

- 格式

  类名::静态方法

- 范例

  Integer::parseInt

  Integer类的方法：public static int parseInt(String s) 将此String转换为int类型数据

- 练习描述

  - 定义一个接口(Converter)，里面定义一个抽象方法 int convert(String s);
  - 定义一个测试类(ConverterDemo)，在测试类中提供两个方法
    - 一个方法是：useConverter(Converter c)
    - 一个方法是主方法，在主方法中调用useConverter方法

- 代码演示

  ```java
  public interface Converter {
      int convert(String s);
  }
  
  public class ConverterDemo {
      public static void main(String[] args) {
  
  		//Lambda写法
          useConverter(s -> Integer.parseInt(s));
  
          //引用类方法
          useConverter(Integer::parseInt);
  
      }
  
      private static void useConverter(Converter c) {
          int number = c.convert("666");
          System.out.println(number);
      }
  }
  ```

- ```java
  package com.itheima.function;
  
  import java.util.ArrayList;
  import java.util.Collections;
  
  public class FunctionDemo2 {
      public static void main(String[] args) {
          /*
              方法引用(引用静态方法)
              格式:
                  类名::方法名
  
              需求:
                  集合中有一下数字,要求把他们都变成int类型
                  "1","2","3","4","5"
           */
  
          //1.创建集合并添加元素
          ArrayList<String> list = new ArrayList<>();
          Collections.addAll(list,"1","2","3","4","5");
  
          //2.把他们都变成int类型
         /* list.stream().map(new Function<String, Integer>() {
              @Override
              public Integer apply(String s) {
                  int i = Integer.parseInt(s);
                  return i;
              }
          }).forEach(s -> System.out.println(s));*/
  
  
          //1.方法需要已经存在
          //2.方法的形参和返回值需要和抽象方法的形参和返回值保持一致
          //3.方法的功能需要把形参的字符串转换为整数
          list.stream()
                  .map(Integer::parseInt)
                  .forEach(s -> System.out.println(s));
  
  
      }
  }
  
  ```
  
- 使用说明

  Lambda表达式被类方法替代的时候，它的形式参数全部传递给静态方法作为参数

### 3.4引用对象的实例方法(引用成员方法)【应用】

​	引用对象的实例方法，其实就引用类中的成员方法

- 格式

  对象::成员方法

  1. 其他类:	其他类对象::方法名
  2. 本类:        this::方法名 (详见day26 game)
  3. 父类:        super::方法名

- 范例

  "HelloWorld"::toUpperCase

    String类中的方法：public String toUpperCase() 将此String所有字符转换为大写

- 练习描述

  - 定义一个类(PrintString)，里面定义一个方法

    public void printUpper(String s)：把字符串参数变成大写的数据，然后在控制台输出

  - 定义一个接口(Printer)，里面定义一个抽象方法

    void printUpperCase(String s)

  - 定义一个测试类(PrinterDemo)，在测试类中提供两个方法

    - 一个方法是：usePrinter(Printer p)
    - 一个方法是主方法，在主方法中调用usePrinter方法

- 代码演示

  ```java
  public class PrintString {
      //把字符串参数变成大写的数据，然后在控制台输出
      public void printUpper(String s) {
          String result = s.toUpperCase();
          System.out.println(result);
      }
  }
  
  public interface Printer {
      void printUpperCase(String s);
  }
  
  public class PrinterDemo {
      public static void main(String[] args) {
  
  		//Lambda简化写法
          usePrinter(s -> System.out.println(s.toUpperCase()));
  
          //引用对象的实例方法
          PrintString ps = new PrintString();
          usePrinter(ps::printUpper);
  
      }
  
      private static void usePrinter(Printer p) {
          p.printUpperCase("HelloWorld");
      }
  }
  
  ```

- ```java
  package com.itheima.function;
  
  import java.util.ArrayList;
  import java.util.Collections;
  
  public class FunctionDemo3 {
      public static void main(String[] args) {
          /*
              方法引用(引用成员方法)
              格式
                  其他类: 其他类对象::方法名
                  本类: this::方法名(引用处不能是静态方法)
                  父类: super::方法名(引用处不能是静态方法)
  
              需求:
                  集合中有一些名字,按照要求过滤
                  数据:"张无忌","周芷若","赵敏","张强","张三丰"
                  要求:只要张开头,而且名字是3个字的
           */
  
          //1.创建集合
          ArrayList<String> list = new ArrayList<>();
          //2.添加数据
          Collections.addAll(list, "张无忌", "周芷若", "赵敏", "张强", "张三丰");
          //3.过滤数据(只要张开头,而且名字是3个字的)
          /*list.stream()
                  //.filter(s -> s.startsWith("张") && s.length() == 3)
                  .filter(s -> s.startsWith("张"))
                  .filter(s -> s.length() == 3)
                  .forEach(s -> System.out.println(s));*/
  
          /*list.stream().filter(new Predicate<String>() {
              @Override
              public boolean test(String s) {
                  return s.startsWith("张") && s.length() == 3;
              }
          }).forEach(s -> System.out.println(s));*/
  
          /*StringOperation so = new StringOperation();
          list.stream()
                  .filter(so::stringJudge)
                  .forEach(s -> System.out.println(s));*/
  
          //静态方法中没有this的
          list.stream()
                  .filter(new FunctionDemo3()::stringJudge)
                  .forEach(s -> System.out.println(s));
  
      }
  
      public boolean stringJudge(String s){
          return s.startsWith("张") && s.length() == 3;
      }
  }
  
  ```
  
- 使用说明

  Lambda表达式被对象的实例方法替代的时候，它的形式参数全部传递给该方法作为参数

### 3.5引用构造器(引用构造方法)【应用】

​	引用构造器，其实就是引用构造方法

- 格式

  类名::new

- 范例

  Student::new

- 练习描述

  - 定义一个类(Student)，里面有两个成员变量(name,age)

    并提供无参构造方法和带参构造方法，以及成员变量对应的get和set方法

  - 定义一个接口(StudentBuilder)，里面定义一个抽象方法

    Student build(String name,int age);

  - 定义一个测试类(StudentDemo)，在测试类中提供两个方法

    - 一个方法是：useStudentBuilder(StudentBuilder s)
    - 一个方法是主方法，在主方法中调用useStudentBuilder方法

- 代码演示

  ```java
  public class Student {
      private String name;
      private int age;
  
      public Student() {
      }
  
      public Student(String name, int age) {
          this.name = name;
          this.age = age;
      }
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  }
  
  public interface StudentBuilder {
      Student build(String name,int age);
  }
  
  public class StudentDemo {
      public static void main(String[] args) {
  
  		//Lambda简化写法
          useStudentBuilder((name,age) -> new Student(name,age));
  
          //引用构造器
          useStudentBuilder(Student::new);
  
      }
  
      private static void useStudentBuilder(StudentBuilder sb) {
          Student s = sb.build("林青霞", 30);
          System.out.println(s.getName() + "," + s.getAge());
      }
  }
  ```

- ```java
  package com.itheima.function;
  
  import java.util.ArrayList;
  import java.util.Collections;
  import java.util.List;
  import java.util.stream.Collectors;
  
  public class FunctionDemo4 {
      public static void main(String[] args) {
          /*
          方法引用(引用构造方法)
          格式
                  类名::new
  
          目的:
                  创建这个类的对象
  
          需求:
                  集合里面存储姓名和年龄,要求封装成Student对象并收集到List集合中
  
          方法引用规则:
              1.需要函数式接口
              2.被引用的方法必须已经存在
              3.被引用方法的形参和返回值,需要跟抽象方法的形参和返回值保持一致
              4.被引用方法的功能需要满足当前的需求
           */
  
          //1.创建集合对象
          ArrayList<String> list = new ArrayList<>();
  
          //2.添加数据
          Collections.addAll(list,"张无忌-15","周芷若-14","赵敏-13","张强-20","张三丰-100","张翠山-40","张良-35","王二麻子-37","谢广坤-41");
  
          //3.要求封装成Student对象并收集到List集合中
          //String -> Student
          /*List<Student> newList = list.stream().map(new Function<String, Student>() {
              @Override
              public Student apply(String s) {
                  String[] arr = s.split("-");
                  String name = arr[0];
                  int age = Integer.parseInt(arr[1]);
                  return new Student(name, age);
              }
          }).collect(Collectors.toList());
  
          System.out.println(newList);*/
  
          List<Student> newList2 = list.stream().map(Student::new).collect(Collectors.toList());
          System.out.println(newList2);
  
      }
  }
  
  ```
  
- ```java
  package com.itheima.function;
  
  public class Student {
      private String name;
      private int age;
  
  
      public Student() {
      }
  
      public Student(String str) {
          String[] arr = str.split("-");
          this.name = arr[0];
          this.age = Integer.parseInt(arr[1]);
      }
  
      public Student(String name, int age) {
          this.name = name;
          this.age = age;
      }
  
      /**
       * 获取
       * @return name
       */
      public String getName() {
          return name;
      }
  
      /**
       * 设置
       * @param name
       */
      public void setName(String name) {
          this.name = name;
      }
  
      /**
       * 获取
       * @return age
       */
      public int getAge() {
          return age;
      }
  
      /**
       * 设置
       * @param age
       */
      public void setAge(int age) {
          this.age = age;
      }
  
      public String toString() {
          return "Student{name = " + name + ", age = " + age + "}";
      }
      public String forString() {
          return name + "-" + age;
      }
  }
  
  ```
  
- 使用说明

  Lambda表达式被构造器替代的时候，它的形式参数全部传递给构造器作为参数

### 3.6引用类的实例方法【应用】

​	引用类的实例方法，其实就是引用类中的成员方法

- 格式

  类名::成员方法

- 范例

  String::substring

  public String substring(int beginIndex,int endIndex) 

  从beginIndex开始到endIndex结束，截取字符串。返回一个子串，子串的长度为endIndex-beginIndex

- 练习描述

  - 定义一个接口(MyString)，里面定义一个抽象方法：

    String mySubString(String s,int x,int y);

  - 定义一个测试类(MyStringDemo)，在测试类中提供两个方法

    - 一个方法是：useMyString(MyString my)
    - 一个方法是主方法，在主方法中调用useMyString方法

- 代码演示

  ```java
  public interface MyString {
      String mySubString(String s,int x,int y);
  }
  
  public class MyStringDemo {
      public static void main(String[] args) {
  		//Lambda简化写法
          useMyString((s,x,y) -> s.substring(x,y));
  
          //引用类的实例方法
          useMyString(String::substring);
  
      }
  
      private static void useMyString(MyString my) {
          String s = my.mySubString("HelloWorld", 2, 5);
          System.out.println(s);
      }
  }
  ```

- ```java
  package com.itheima.function;
  
  import java.util.ArrayList;
  import java.util.Collections;
  
  public class FunctionDemo5 {
      public static void main(String[] args) {
          /*
              方法引用(类名引用成员方法)
              格式
                  类名::成员方法
  
              需求:
                  集合里面一些字符串,要求变成大写后进行输出
  
              方法引用的规则:
              1.需要有函数式接口
              2.被引用的方法必须已经存在
              3.被引用方法的形参,需要跟抽象方法的第二个形参到最后一个形参保持一致,返回值需要保持一致
              4.被引用方法的功能需要满足当前的需求
  
              抽象方法形参的详解:
              第一个参数:表示被引用方法的调用者,决定了可以引用哪些类中的方法
                        在Stream流中,第一个参数一般都表示流里面的每一个数据
                        假设流里面的数据是字符串,那么使用这种方式进行方法引用,只能引用String这个类中的方法
  
              第二个参数到最后一个参数:跟被引用方法的形参保持一致,如果没有第二个参数,说明被引用的方法需要是无参的成员方法
  
              局限性:
                  不能引用所有类中的成员方法
                  是跟抽象方法的第一个参数有关,这个参数是什么类型的,那么就只能引用这个类中的方法
  
           */
  
          //1.创建集合对象
          ArrayList<String> list = new ArrayList<>();
  
          //2.添加数据
          Collections.addAll(list, "aaa", "bbb", "ccc", "ddd");
  
          //3.变成大写后进行输出
          //map(String::toUpperCase)
          //拿着流里面的每一个数据,去调用,去调用String类中的toUpperCase方法,方法的返回值就是转换之后的结果
          list.stream().map(String::toUpperCase).forEach(s -> System.out.println(s));
  
  
          //String -> String
         /* list.stream().map(new Function<String, String>() {
              @Override
              public String apply(String s) {
                  return s.toUpperCase();
              }
          }).forEach(s -> System.out.println(s));*/
  
  
      }
  }
  
  ```
  
- 使用说明

  ​    Lambda表达式被类的实例方法替代的时候
  ​    第一个参数作为调用者
  ​    后面的参数全部传递给该方法作为参数

### 3.7引用数组的构造方法【应用】

- 格式: 

  数据类型[]::new

- 范例:

  int[]::new

- 练习描述

  集合中存储一些整数,收集到数组当中
  
  ```java
  package com.itheima.function;
  
  import java.util.ArrayList;
  import java.util.Arrays;
  import java.util.Collections;
  
  public class FunctionDemo6 {
      public static void main(String[] args) {
          /*
          方法引用(数组的构造方法)
          格式:
                  数组类型[]::new
  
          目的:
                  创建一个指定类型的数组
  
          需求:
                  集合中存储一些整数,收集到数组当中
  
          细节:
              数组的类型,需要跟流中的数据类型保持一致
           */
  
  
          //1.创建集合并添加元素
          ArrayList<Integer> list = new ArrayList<>();
          Collections.addAll(list,1,2,3,4,5);
  
          //2.收集到数组当中
          Integer[] arr2 = list.stream().toArray(Integer[]::new);
  
  
          /*Integer[] arr = list.stream().toArray(new IntFunction<Integer[]>() {
              @Override
              public Integer[] apply(int value) {
                  return new Integer[value];
              }
          });*/
  
          //3.打印
          System.out.println(Arrays.toString(arr2));
      }
  }
  
  ```
  
## 总结

1.什么是方法引用?

把已经存在的方法拿过来用,当做函数式接口中抽象方法的方法体

2.:: 是什么符号?

方法引用符

3.方法引用时要注意什么?

- 需要有函数式接口
- 被引用方法必须已经存在
- 被引用方法的形参和返回值需要跟抽象方法保持一致
- 被引用方法的功能要满足当前需求

(1) 引用静态方法

​	类名 :: 静态方法

(2) 引用成员方法

​	对象 :: 成员方法

​	this :: 成员方法

​	super :: 成员方法

(3) 引用构造方法

​	类名 :: new

(4) 使用类名引用成员方法

​	类名 :: 成员方法 (==不能引用所有类中的成员方法,如果抽象方法的第一个参数是A类型的,只能引用A类中的方法==)

(5) 引用数组的构造方法

​	数据类型[] :: new

## 练习

```java
package com.itheima.function;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;

public class FunctionDemo7 {
    public static void main(String[] args) {
        /*
        需求:
            集合中存储一些字符串的数据,比如:张三,23
            收集到Student类型的数组当中
         */

        //1.创建集合并添加元素
        ArrayList<String> list = new ArrayList<>();
        Collections.addAll(list, "张无忌-15", "周芷若-14", "赵敏-13", "张强-20", "张三丰-100", "张翠山-40", "张良-35", "王二麻子-37", "谢广坤-41");

        //2.先把字符串变成Student对象,然后再把Student对象收集起来
        /*Student[] arr = list.stream().map(new Function<String, Student>() {
            @Override
            public Student apply(String s) {
                String name = s.split("-")[0];
                int age = Integer.parseInt(s.split("-")[1]);
                return new Student(name, age);
            }
        }).toArray(new IntFunction<Student[]>() {
            @Override
            public Student[] apply(int value) {
                return new Student[value];
            }
        });*/

        //3.打印数组
        Student[] arr2 = list.stream().map(Student::new).toArray(Student[]::new);


        System.out.println(Arrays.toString(arr2));


    }
}
```

```java
package com.itheima.function;

import java.util.ArrayList;
import java.util.Arrays;

public class FunctionDemo8 {
    public static void main(String[] args) {
        /*
        需求:
            创建集合添加学生对象
            学生对象属性:name,age

        要求:
            获取姓名并放到数组中
            使用方法引用完成

        技巧:
            1.现在有没有一个方法符合我当前的需求
            2.如果有这样的方法,这个方法是否满足引用的规则
            静态  类名::方法
            成员方法
            构造方法
            3.
         */

        //1.创建集合
        ArrayList<Student> list = new ArrayList<>();
        //2.添加元素
        list.add(new Student("zhangsan",23));
        list.add(new Student("lisi",24));
        list.add(new Student("wangwu",25));
        //3.获取姓名并放到数组中
        //有没有这样的一个方法满足我的要求
        //对象::方法名
        //类名::方法名   被引用的方法形参是跟抽象方法第二个形参后面保持一致
        String[] arr = list.stream().map(Student::getName).toArray(String[]::new);


        /*String[] arr = list.stream().map(new Function<Student, String>() {
            @Override
            public String apply(Student student) {
                return student.getName();
            }
        }).toArray(new IntFunction<String[]>() {
            @Override
            public String[] apply(int value) {
                return new String[value];
            }
        });*/
        System.out.println(Arrays.toString(arr));

        /*String[] arr = list.stream().map(new Function<Student, String>() {
            @Override
            public String apply(Student student) {
                return student.getName();
            }
        }).toArray(String[]::new);
        System.out.println(Arrays.toString(arr));*/
    }
}

```

