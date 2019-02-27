### API

#### 获取角色列表

```http
GET /v1/roles
```

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no|排序规则||
|page|int|no|||
|per_page|int|no|||
|columns|string|no|字段筛选|列和子列的选择|

eg: /v1/roles?columns=role_id,name,org_id,org.name

返回结果：

    Status: 200 OK
    {
        "users": [
            { # 参见 UserInfo
              "role_id": "",
              "org_id": ,
              "name": "",
              "org": {...},
              "creator": {...},
              "status": 1/2,
              "created": "",
              "updated": "",
              "company": {...},
            },
            ...
        ]
    }

新增角色role

```http
POST /v1/roles
```

表单:

| Name       | Type   | Required | Default | Description                                                  |
| ---------- | ------ | -------- | ------- | ------------------------------------------------------------ |
| name       | string | yes      |         | role 名字                                                    |
| company_id | int    | no       |         |                                                              |
| org_id     | int    | yes      |         | subordinate department的id, 如果没有, 就使用superior department 的id |

响应:

```json
Status: 200 OK
{
    "created": 时间戳乘以1000, 
    "role_id": 新增的role id
}
```

#### 查看role的属性值

```http
GET /v1/roles/<role_id>
```

响应:

```json
{
    "actions": [], 
    "company_id": null, 
    "created": 1541488635000, 
    "creator": "204", 
    "modules": [], 
    "name": "*****", 
    "org": {}, 
    "org_id": 35, 
    "resources": [], 
    "role_id": 168, 
    "status": 1, 
    "updated": 1541488635000
}
```

#### 修改role的属性值

```http
PUT /v1/roles/<role_id>
```

表单:

| Name | Type   | Required | Default | Description  |
| ---- | ------ | -------- | ------- | ------------ |
| name | string | yes      |         | role的新名字 |

响应:

```json
Status: 200 OK
""
```

#### 修改role的权限范围

```http
PUT /v1/roles/<role_id>/access
```

表单:

| Name      | Type   | Required | Default | Description      |
| --------- | ------ | -------- | ------- | ---------------- |
| modules   | string | no       |         | 设置能访问的模块 |
| actions   | string | no       |         | 设置操作权限     |
| resources | string | no       |         | 涉及到的实体类型 |

响应:

```json
Status: 200 OK
""
```

