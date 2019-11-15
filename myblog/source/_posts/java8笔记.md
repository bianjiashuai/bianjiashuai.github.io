---
title: java8笔记
date: 2019-11-15 15:04:22
tags:
---

### 1、Collectors 类的静态工厂方法

* **toList：把流中所有项目收集到一个 List**
  返回类型为：`List<T>`

  ```java
  List<Dish> dishes = menuStream.collect(toList());
  ```

* **toSet：把流中所有项目收集到一个 Set ，删除重复项**
  返回类型为：`Set<T>`

  ```java
  Set<Dish> dishes = menuStream.collect(toSet());
  ```

* **toCollection：把流中所有项目收集到给定的供应源创建的集合**
  返回类型为：`Collection<T>`

  ```java
  Collection<Dish> dishes = menuStream.collect(toCollection(), ArrayList::new);
  ```

* **counting：计算流中元素的个数**
  返回类型为：`Long`

  ```java
  long howManyDishes = menuStream.collect(counting());
  ```

* **summingInt：对流中项目的一个整数属性求和**
  返回类型为：`Integer`

  ```java
  int totalCalories = menuStream.collect(summingInt(Dish::getCalories));
  ```

* **averagingInt：计算流中项目 Integer 属性的平均值**
  返回类型为：`Double`

  ```java
  double avgCalories = menuStream.collect(averagingInt(Dish::getCalories));
  ```

* **summarizingInt：收集关于流中项目 Integer 属性的统计值，例如最大、最小、总和与平均值**
  返回类型为：`IntSummaryStatistics`

  ```java
  IntSummaryStatistics menuStatistics = 			 
  	menuStream.collect(summarizingInt(Dish::getCalories));
  ```

* **joining：连接对流中每个项目调用 toString 方法所生成的字符串**
  返回类型为：`String`

  ```java
  String shortMenu = menuStream.map(Dish::getName).collect(joining(", "));
  ```

* **maxBy：一个包裹了流中按照给定比较器选出的最大元素的 Optional，或如果流为空则为Optional.empty()**
  返回类型为：`Optional<T>`

  ```
  Optional<Dish> fattest = 	
  	menuStream.collect(maxBy(comparingInt(Dish::getCalories)));
  ```

* **minBy：一个包裹了流中按照给定比较器选出的最小元素的 Optional，或如果流为空则为Optional.empty()**
  返回类型为：`Optional<T>`

  ```java
  Optional<Dish> lightest= 
  	menuStream.collect(minBy(comparingInt(Dish::getCalories)));
  ```

* **reducing：从一个作为累加器的初始值开始，利用 BinaryOperator 与流中的元素逐个结合，从而将流归约为单个值**
  返回类型为：`归约操作产生的类型`

  ```java
  int totalCalories = menuStream.collect(reducing(0, Dish::getCalories, 
  	Integer::sum));
  ```

* **collectingAndThen：包裹另一个收集器，对其结果应用转换函数**
  返回类型为：`转换函数返回的类型`

  ```java
  int howManyDishes = menuStream.collect(collectingAndThen(toList(), List::size));
  ```

* **groupingBy：根据项目的一个属性的值对流中的项目作问组，并将属性值作为结果 Map 的键**
  返回类型为：`Map<K, List<T>>`

  ```java
  Map<Dish.Type, List<Dish>> dishesByType = 
  	menuStream.collect(groupingBy(Dish::getType));
  ```

* **partitioningBy：根据对流中每个项目应用谓词的结果来对项目进行分区**

  返回类型为：`Map<Boolean, List<T>>>`

  ```java
  Map<Boolean, List<Dish>> vegetarianDishes = 
  	menuStream.collect(partitioningBy(Dish::isVegetarian);
  ```

### 2、Java 8中的常用函数式接口

| **函数式接口**          | **函数描述符**      | **原始类型特化**                                             |
| ----------------------- | ------------------- | ------------------------------------------------------------ |
| **Predicate<T>**        | **T->boolean**      | **IntPredicate** <br />**LongPredicate** <br />**DoublePredicate** |
| **Consumer<T>**         | **T->void**         | **IntConsumer** <br />**LongConsumer** <br />**DoubleConsumer** |
| **Function<T, R>**      | **T->R**            | **IntFunction<R>** <br />**IntToDoubleFunction** <br />**IntToLongFunction** <br /><br />**LongFunction<R>** <br />**LongToDoubleFunction** <br />**LongToIntFunction** <br /><br />**DoubleFunction<R>** <br /><br />**ToIntFunction<T>**, <br />**ToDoubleFunction<T>**, <br />**ToLongFunction<T>** |
| **Supplier<T>**         | **()->T**           | **BooleanSupplier**<br />**IntSupplier**<br />**LongSupplier**<br />**DoubleSupplier** |
| **UnaryOperator<T>**    | **T->T**            | **IntUnaryOperator**<br />**LongUnaryOperator**<br />**DoubleUnaryOperator** |
| **BinaryOperator<T>**   | **(T, T)->T**       | **IntBinaryOperator**<br />**DoubleBinaryOperator**<br />**LongBinaryOperator** |
| **BiPredicate<L, R>**   | **(L, R)->boolean** |                                                              |
| **BiConsumer<T, U>**    | **(T, U)->void**    | **ObjIntConsumer<T>**<br />**ObjDoubleConsumer<T>**<br />**ObjLongConsumer<T>** |
| **BiFunction<T, U, R>** | **(T, U)->R**       | **ToIntBiFunction<T, U>**<br />**ToLongBiFunction<T, U>**<br />**ToDoubleBiFunction<T, U>** |

### 3、Optional 类的方法

| **方法**        | **描述**                                                     |
| --------------- | ------------------------------------------------------------ |
| **empty**       | 返回一个空的 Optional 实例                                   |
| **filter**      | 如果值存在并且满足提供的谓词，就返回包含该值的 Optional 对象；否则返回一个空的Optional 对象 |
| **flatMap**     | 如果值存在，就对该值执行提供的 mapping 函数调用，返回一个 Optional 类型的值，否则就返回一个空的 Optional 对象 |
| **get**         | 如果该值存在，将该值用 Optional 封装返回，否则抛出一个 NoSuchElementException 异常 |
| **ifPresent**   | 如果值存在，就执行使用该值的方法调用，否则什么也不做         |
| **isPresent**   | 如果值存在就返回 true ，否则返回 false                       |
| **map**         | 如果值存在，就对该值执行提供的 mapping函数调用               |
| **of**          | 将指定值用 Optional 封装之后返回，如果该值为 null ，则抛出一个 NullPointerException异常 |
| **ofNullable**  | 将指定值用 Optional 封装之后返回，如果该值为 null ，则返回一个空的 Optional 对象 |
| **orElse**      | 如果有值则将其返回，否则返回一个默认值                       |
| **orElseGet**   | 如果有值则将其返回，否则返回一个由指定的 Supplier 接口生成的值 |
| **orElseThrow** | 如果有值则将其返回，否则抛出一个由指定的 Supplier 接口生成的异常 |

### 4、Spliterator 的特性

| **特性**       | **含义**                                                     |
| -------------- | ------------------------------------------------------------ |
| **ORDERED**    | 元素有既定的顺序（例如 List ），因此 Spliterator 在遍历和划分时也会遵循这一顺序 |
| **DISTINCT**   | 对于任意一对遍历过的元素 x 和 y ， x.equals(y) 返回 false    |
| **SORTED**     | 遍历的元素按照一个预定义的顺序排序                           |
| **SIZED**      | 该 Spliterator 由一个已知大小的源建立（例如 Set ），因此 estimatedSize() 返回的是准确值 |
| **NONNULL**    | 保证遍历的元素不会为 null                                    |
| **IMMUTABLE**  | Spliterator 的数据源不能修改。这意味着在遍历时不能添加、删除或修改任何元素 |
| **CONCURRENT** | 该 Spliterator 的数据源可以被其他线程同时修改而无需同步      |
| **SUBSIZED**   | 该 Spliterator 和所有从它拆分出来的 Spliterator 都是 SIZED   |

