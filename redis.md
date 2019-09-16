# redis

## String

### 与C++String区别

C++String不记录长度，需要遍历

C++String以"\0"结尾，所以不能存储换行符

### redis Hash String性能

hash性能更高，但不支持对hkey做超时，只能对整个hash做
但String型能水平拓展，能做集群降低单机压力

## Redis数据类型

String 基本类型，部分操作可以尝试将字符串解析为数字

Set

List

Hash hash表

Zset 有序集合，可以根据排序后的结果返回，也可以做范围查询

## 集群模式

主从/哨兵

集群

## Redis和数据库的一致性

一致性要求低可以使用两次删除

一致性要求高采用队列，并哈希至同一个工作线程

[redis缓存与数据库一致性问题解决](https://blog.csdn.net/qq_27384769/article/details/79499373)

[redis系列之数据库与缓存数据一致性解决方案](https://www.cnblogs.com/cxxjohnson/p/8519616.html)





