### API

#### 获取用户状态信息

```http
GET /user/status
```

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|email|string|yes||输入的邮箱|

返回结果：

```json
Status: 200 OK
{
	"status": 0 # 0：状态正常，1：用户不存在， 2：用户被disable， 3：用户没有role
}
```

#### 获取用户列表

```http
GET /users
```

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no|排序规则|
|page|int|no||
|per_page|int|no||
|columns|string|no|字段筛选|

eg: /v1/users?columns=user_id,name,roles.role_id,roles.name

返回结果：

```json
Status: 200 OK
{
    "page": 1,
    "per_page": 1,
    "total": 89,
    "users": [
        {
            "created": 1535599129000,
            "creator": null,
            "email": "ang.li@ihandysoft.com",
            "name": "ang.li ",
            "optimizer_id": "T08503",
            "roles": [],
            "status": 1,
            "updated": 1535596125000,
            "user_id": 1
        }
    ]
}
```

#### 新增用户

```http
POST /v1/users/
```

表单:

| Name         | Type   | Required | Description            |
| ------------ | ------ | -------- | ---------------------- |
| name         | string | yes      | 用户名                 |
| email        | string | yes      | 用户邮箱               |
| role_ids     | string | no       | 在哪些角色下行动       |
| optimizer_id | string | no       | 如果是优化师, 优化师id |

#### 查看当前用户的信息

```http
GET /v1/user
```

#### 查看用户的信息

```http
GET /v1/users/<user_id>
```

```json
Status Code: 200
{
    "created": 1535594849000,
    "creator": {},
    "email": "ning.zhou@ihandysoft.com",
    "name": "ning.zhou",
    "optimizer_id": "",
    "status": 1,
    "updated": 1541411561000,
    "user_id": 120
}
```



#### 修改用户的信息

```http
PUT /v1/users/<user_id>
```

表单同上, 邮箱地址不能变

#### 激活用户

```http
PUT /v1/users/<user_id>/enabled
```

#### 冻结用户

```http
PUT /v1/users/<user_id>/disabled
```



#### 获取部门下的用户列表

下发部门到用户, 其它部门也可以管理权限

```http
GET /orgs/<org_id>/users
```

#### 新增用户

```http
POST /orgs/<org_id>/users
```

#### 查看用户信息

```http
GET /orgs/<org_id>/users/<user_id>
```

#### 修改用户信息

```http
PUT /orgs/<org_id>/users/<user_id>
```

#### 激活用户

```http
PUT /orgs/<org_id>/users/<user_id>/enabled
```

#### 冻结用户

```http
PUT /orgs/<org_id>/users/<user_id>/disabled
```

