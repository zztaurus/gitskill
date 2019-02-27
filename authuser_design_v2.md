### API

#### 获取登录用户信息

```http
GET /user
```
返回结果：

```json
Status: 200 OK
{
    "created": 1535604485000, 
    "created_by": "", 
    "creator": null, 
    "email": "linlin.liu@ihandysoft.com", 
    "name": "linlin.liu ", 
    "optimizer_id": "", 
    "roles": [...]
}
```

#### 切换用户角色

```http
POST /v1/change_role
```

表单:

| Name         | Type   | Required | Description            |
| ------------ | ------ | -------- | ---------------------- |
| role_id      | int    | yes      | 角色id                  |

    Status Code: 200