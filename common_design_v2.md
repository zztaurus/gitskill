### API

group_by 规则: 分组字段按照逗号（“,”）分隔

group_by=date,app_id,country

aggregate 规则：需要进行聚合操作的字段按照逗号（“,”）分隔

kpis=installs;sum:retention_day_1

order_by 规则：多个排序字段按先后顺序用'|'分隔
排序格式如下：sort_name:sort_rule，其中 sort_rule 可以为 0（降序）和 1（升序）

order_by=installs:0|created:1

filter_by 规则：多个筛选条件用`|`分隔，筛选条件为`or`的时候使用`,`分隔，筛选关键字与筛选值之间使用`: 关系词：`表示

关系词如下：

|关系词|意思|是否必须|例子|
|---|---|---|---|
|`$eq`| 筛选关键字对应内容等于筛选值 |no|`field_name:$eq:field_value` 或者 `field_name:field_value`（省略时只加一个`:`)|
|`$gt`| 筛选关键字对应内容大于筛选值 |no|`field_name:$gt:field_value`|
|`$gte`| 筛选关键字对应内容大于等于筛选值 |no|`field_name:$gte:field_value`|
|`$lt`| 筛选关键字对应内容小于筛选值 |no|`field_name:$lt:field_value`|
|`$lte`| 筛选关键字对应内容小于等于筛选值 |no|`field_name:$lte:field_value`|
|`$exists`| 筛选关键字对应内容包含筛选值（完全匹配），用于list |yes|`field_name:$exists:field_value`|
|`$!exists`| 筛选出关键字对应内容包含筛选值的所有记录的差集（完全匹配），用于list|no|`field_name:$exists:field_value`|
|$ne| 筛选关键字对应内容不等于筛选值 |yes|field_name:$ne:field_value|
|$be|  此项是否为空|yes|increases:$be:yes 或者 decreases:$be:yes|
|$like| 模糊匹配 |yes|name:$like:nihao|

格式如下：

    filter_by=field_name1:field_value1|field_name2:field_value2,field_name3:field_value3|
    filter_by=field_name4:$exists:field_value4,field_name5:$exists:field_value5
    filter_by=field_name6:$ne:field_value6,field_name7:$ne:field_value7

示例：/v1/orgs?filter_by=category:1,installs:'$gt':100|org_id:1&group_by=date,app_id,country&order_by=created:0

columns规则：字段间按照逗号（“,”）分隔，查询所有字段使用`*`，不传即为不查询，也可使用`-`表示不查询，默认返回关联对象的id，可使用`-a.*`表示不查询管理表a的全部信息

格式如下：

```
page=1&per_page=1&columns=a,b,c 包含total,包含columns a,b,c
page=1&per_page=10&data=total&columns=a,-b,c  包含total,包含columns a,c不包含b
page=1&per_page=10&data=-total&columns=a,b,c.* 不包含total,包含columns a,b和整个关联对象c
page=1&per_page=10&data=total&columns=a,b,-c.* 包含total,包含columns a,b不包含整个关联对象c
page=1&per_page=10&data=total&columns=a,b,-c.d 包含total,包含columns a,b不包含关联对象c.d
```