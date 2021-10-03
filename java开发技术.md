# java开发技术

* Java 常用函数式接口之Consumer接口

  * java.util.function.Consume
  * 默认方法andThen 作用：需要两个Consumer接口，可以把两个Consumer接口组合到一起再对数据进行消费

* 流处理

  * 2种操作：

    1.intermediate  operation 中间操作：中间操作的结果是刻画、描述了一个Stream，并没有产生一个新集合，这种操作也叫做惰性求值方法。

    2.terminal operation 终止操作：最终会从Stream中得到值。

  * collect(toList()) 终止操作  由Stream中的值生成一个List列表，也可用collect(toSet())生成一个Set集合。

  * map 中间操作

    将一种类型的值映射为另一种类型的值，可以将 Stream 中的每个值都映射为一个新的值，最终转换为一个新的 Stream 流

    ```java
    	@Test
    	public void mapTest() {
    		String[] testStrings = { "java", "react", "angular", "vue" };
     
    		List<String> list = Stream.of(testStrings).map(test -> test.toUpperCase()).collect(Collectors.toList());
     
    		list.forEach(test -> System.out.println(test));
    	}
    ```

    

  * filter 中间操作
    遍历并筛选出满足条件的元素形成一个新的 Stream 流。

    ```java
    	@Test
    	public void filterTest() {
    		List<String> list = Arrays.asList("java", "react", "angular", "javascript", "vue");
    		
    		long count = list.stream().filter(p -> p.startsWith("j")).count();
     
     
    		System.out.println(count);
    	}
    ```

  * flatMap 中间操作
    可用 Stream 替换值，并将多个 Stream 流合并成一个 Stream 流。

    ```java
    	@Test
    	public void flapMapTest() {
    		List<Integer> list = (List<Integer>) Stream.of(Arrays.asList(1, 2, 3, 4, 5, 6), Arrays.asList(8, 9, 10, 11, 12))
    				.flatMap(test -> test.stream()).collect(Collectors.toList());
     
    		for (int i = 0, length = list.size(); i < length; i++) {
    			System.out.println(list.get(i));
    		}
     
    	}
    ```

  * max 、min 终止操作
    求 Stream 中的最大值、最小值。

  * reduce 终止操作
    从 Stream 的一组值中生成另一个值。

  * ![alt 流操作函数](.\img\20200826082206770.png)

* StringBuffer

* Collectors
  * 
  
* JTA，全称：Java Transaction API。JTA事务比JDBC事务更强大。一个JTA事务可以有多个参与者，而一个JDBC事务则被限定在一个单一的数据库连接。所以，当我们在同时操作多个数据库的时候，使用JTA事务就可以弥补JDBC事务的不足。

  * Atomikos：可以通过引入spring-boot-starter-jta-atomikos依赖来使用

* javax.sql.DataSource

  * 实现DataSource接口即必须重写getConnection方法，即可以获得Connection对象，有了Connection对象即可以对数据库操作。
  * https://www.cnblogs.com/noteless/p/10319296.html
  * 数据源作为DriverManager的替代者，用于获取数据库连接，你应该总是使用DataSource
  * DataSource只有两个方法（确切的说是一个方法的两个重载版本），用于建立与此 DataSource 对象所表示的数据源的连接。
    - Connection getConnection()
    - Connection getConnection(String username, String password)

* DriverManager

* 多数据源及其切换

  * AbstractRoutingDataSource
  * https://segmentfault.com/a/1190000021613404
  * 事务模式，为啥不能切换数据源
    * Spring的自动事务是基于AOP实现的。在调用包含事务的方法时，会进入一个拦截器。
    * https://juejin.cn/post/6844904159074844685
  * 多数据支持事务
    * https://www.cnblogs.com/red-star/p/12535919.html
    * 多数据源事务切面

* 枚举

  * enum
  
* 逻辑删除

  * ```bash
    mybatis-plus:
      global-config:
        db-config:
          # 1 代表已删除，不配置默认是1，也可修改配置
          logic-delete-value: 1
          # 0 代表未删除，不配置默认是0，也可修改配置
          logic-not-delete-value: 0
    ```

  * 在实体类对应的字段上加上注解@TableLogic即可。

* 分层领域模型规约：

  - DO（ Data Object）：与数据库表结构一一对应，通过DAO层向上传输数据源对象。
  - DTO（ Data Transfer Object）：数据传输对象，Service或Manager向外传输的对象。
  - BO（ Business Object）：业务对象。 由Service层输出的封装业务逻辑的对象。
  - AO（ Application Object）：应用对象。 在Web层与Service层之间抽象的复用对象模型，极为贴近展示层，复用度不高。
  - VO（ View Object）：显示层对象，通常是Web向模板渲染引擎层传输的对象。
  - POJO（ Plain Ordinary Java Object）：在本手册中， POJO专指只有setter/getter/toString的简单类，包括DO/DTO/BO/VO等。
  - Query：数据查询对象，各层接收上层的查询请求。 注意超过2个参数的查询封装，禁止使用Map类来传输。
  - 领域模型命名规约：

  - 数据对象：xxxDO，xxx即为数据表名。
  - 数据传输对象：xxxDTO，xxx为业务领域相关的名称。
  - 展示对象：xxxVO，xxx一般为网页名称。
  - POJO是DO/DTO/BO/VO的统称，禁止命名成xxxPOJO。

* DataSourceAutoConfiguration

* LinkedHashMap

  * LinkedHashMap就闪亮登场了，它虽然增加了时间和空间上的开销，但是通过维护一个运行于所有条目的双向链表，LinkedHashMap保证了元素迭代的顺序。该迭代顺序可以是插入顺序或者是访问顺序。

  * | **关  注  点**                | **结    论**                 |
    | ----------------------------- | ---------------------------- |
    | LinkedHashMap是否允许空       | Key和Value都允许空           |
    | LinkedHashMap是否允许重复数据 | Key重复会覆盖、Value允许重复 |
    | LinkedHashMap是否有序         | **有序**                     |
    | LinkedHashMap是否线程安全     | 非线程安全                   |

