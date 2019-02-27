### API

#### 获取media列表

```http
GET /medias
```

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter\_by|string|no||筛选|
|order\_by|string|no|排序规则|
|page|int|no||
|per\_page|int|no||
|columns|string|no|字段筛选|

返回结果：

```json
Status: 200 OK
{
    "page": 1,
    "per_page": 1,
    "nmedias": [
        {
            "media_id": xxx,
            "name": "xxx",
            "alias": "xxx",
            "created": 1520579403000,
            "updated": 1541221796000,
        }
    ],
    "total": 95
}
```

### Model

#### Media

| field       | type        | description | unique | index | NULL |      |
| ----------- | ----------- | ----------- | ------ | ----- | ---- | ---- |
| media_id    | integer     | 主键        | yes    | yes   | no   |      |
| name        | varchar(50) | 邮箱地址    | no     | yes   | no   |      |
| alias       |  varchar(50)| 别名       | no     | yes   | yes  |      |
| updated     | datetime    | 更新时间    | no     | yes   | no   |      |
| created     | datetime    | 创建时间    | no     | yes   | no   |      |



