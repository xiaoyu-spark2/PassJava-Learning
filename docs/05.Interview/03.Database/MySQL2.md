https://blog.csdn.net/weixin_37968613/article/details/114652178

**const**： 根据主键、普通唯一索引列等值匹配查询（is null除外），这种查询是很快的，查询速率认为是常数级别的，定义为const。
**ref** ： 根据普通索引等值匹配，或is null。（前面说的普通唯一索引列查询时 is null也是这种场景）。这种方式需要先根据普通索引匹配到多个主键，然后根据主键进行回表。
**range**：根据主键索引或普通索引（包含唯一索引）进行范围查找
**index**：索引覆盖，你查询的列刚好是索引列，即使查询条件是联合索引的非最左索引列，查询的条件是联合索引中的列，也可能会走索引覆盖
**ALL**: 全表扫描，直接扫描主键索引，这种访问方式称为all。
**index merge** ： 除此之外，还会有index merge（索引合并），针对一些and、or的操作，单纯的回表可能速度会慢一些，如果先将使用到的索引先进行求 交集、并集之后在进行回表，会更加高效。