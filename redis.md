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

