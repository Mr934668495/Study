### 分析SQL语句关键字
Explain  语句

一些参数含义：

id：执行编号，表示SELECT所属的行。如果SQL语句中没有子查询或者关联查询，那么id只有唯一的1，如果有子查询和关联查询，那么就会有多个id。

select_type：标志本行是简单查询还是其他复杂查询

table：标识本行查询是访问了哪个表

type：标识本行查询优化器会使用什么方式进行查询，这个很重要，是我们进行分析的重点内容。

possible_key：标识本行查询可以使用到的全部索引

key：标识本次查询真实使用的索引，这个也很重要

key_len：标识本次查询使用索引的长度，单位是字节数

ref：标识使用索引查询时，使用了那种数据值进行选择，可以是常量，也可以是其余表的字段值

row：显示本次查询会有多少行结果被影响

Extra：一些额外信息，但也很重要


### 关键字执行顺序

FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> DISTINCT -> UNION -> ORDER BY
