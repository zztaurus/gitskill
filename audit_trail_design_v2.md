### API

#### 获取操作记录

    GET /trails

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer|no|1|页号|
|per_page|integer|no|10|每页条数|
|order_by|string|no|排序规则|
|filter_by|string|no||筛选|

返回结果：

    Status: 200 OK
    {
        "trails": [
            { # 参见 TrailInfo
              "trail_id": "",
              "email": "xxx"，
              "description": "",
              "created": "",
              "operators": ["view"],
            },
            ...
        ],
        "page": ,
        "per_page": ,
        "total": ,
    }


### Model

#### AuditTrail

| field       | type        | description | unique | index | NULL |      |
| ----------- | ----------- | ----------- | ------ | ----- | ---- | ---- |
| trail_id    | integer     | 主键        | yes    | yes   | no   |      |
| email       | varchar(50) | 邮箱地址    | no     | yes   | no   |      |
| user_id     | integer     | 用户id      | no     | yes   | yes  |      |
| before      | json dict   | 修改之前    | no     | no    | yes  |      |
| after       | json dict   | 修改之后    | no     | no    | yes  |      |
| description | text        | 备注        | no     | no    | yes  |      |
| created     | datetime    | 创建时间    | no     | yes   | no   |      |

