## ES中的基本数据类型有哪些

![es数据类型](..\imgs\es数据类型.jpg)



[官网数据类型介绍](https://www.elastic.co/guide/en/elasticsearch/reference/6.4/mapping-types.html)

1. 字符串类型

   1. text
   2. keyword

2. 数字类型

   1. long
   2. integer
   3. short
   4. byte
   5. double
   6. float
   7. half_float
   8. scaled_float

3. 日期

   1. date
   2. date_nanos

4. 布尔类型

   1. boolean

5. 二进制

   1. binary

6. 范围

   1. integer/float/long/double/date_range

7. 复杂数据类型

   1. Object
   2. nested

8. 地理数据类型

   1. geo_point
   2. geo_shape

9. 特殊数据类型

   1. ip
   2. ...

10. 数组

    1. 任何字段都可以包含一个或多个值

11. multi-fields

    1. 一个字段可以同时被映射为text用作全文索引，也可以被映射为keyword用于排序和聚合

       