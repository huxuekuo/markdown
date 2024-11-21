# Explain

我们通过MySQL 提供的[Understanding the Query Execution Plan](https://dev.mysql.com/doc/refman/8.4/en/execution-plan-information.html) 文档学习 `explain`语句。

`MySQL`优化器会考虑多种技术来完成`SQL`的查询。

`expalain`可以在不读取所有行的情况下对一个巨大的表执行查询，可以再不比较每一行组合的情况下执行涉及多表的链接查询。---- 这就是`Explain`计划。

**Explain简介**

- `Explain`适用于`Select`/`Insert`/`Delete`/`Update`/`REPLACE`语句。
- `Explain`为`Select`语句中使用的每一张表返回一行数据，按照`MySQL`的执行顺序列出表信息。

## Explain column

```sql
Mysql > explain select * from ac_coin_record;
+----+-------------+----------------+------+---------------+------+---------+------+-------+-------+
| id | select_type | table          | type | possible_keys | key  | key_len | ref  | rows  | Extra |
+----+-------------+----------------+------+---------------+------+---------+------+-------+-------+
|  1 | SIMPLE      | ac_coin_record | ALL  | NULL          | NULL | NULL    | NULL | 34508 | NULL  |
+----+-------------+----------------+------+---------------+------+---------+------+-------+-------+
1 row in set (0.01 sec)
```

`Explain`一共10个字段, 我们将对这10个字段逐一介绍。

**ID**

- 默认是查询顺序, 如果当前行**引用了其他行的并集结果,内容就会为NULL**

**select_type**

- 每行查询类型。

1. Simple : 简单Select, 不适用Union或子查询等。
2. Primary : 查询中包含任何复杂的子部分, 最外层select会被标记为 Primary。
3. Union ：Union 中的第二个或者后面的select语句