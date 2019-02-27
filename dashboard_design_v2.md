#### 获取 view 列表

```http
GET /dashboard/views
```

返回结果：

```json
Status: 200 OK
{
    "templates": [
        {
            "dimension": "Optimizer",
            "template": [
                "*optimizer_id*"
            ]
        }, ....
    ],
    "views": [
        {
            "dimensions": [
                "Agency Type",
                "Month",
                "Payee",
                "Media",
                "Advertiser Company",
                "Advertiser Department",
                "APP Category",
                "APP Name"
            ],
            "mode_view_id": "8150332fa7ea",
            "view_category": "mode",
            "view_id": 1,
            "view_name": "Monthly Media Reporting"
        }, ....
    ]
}
```

#### 生成mode 的视图url

传入ID的字段: 

- Advertiser Company,
- Payee, Department
- Optimizer Team
- Media Buy Agency

 传入name的字段: 

- Agency Type
- Country
- Date
- Media
- App Name
- Optimizer

```http
GET /dashboard/user/roles/<role_id/views/<view_id>/url
```

 请求参数：

| Name   | Type   | Required | Default Value | Description                                          |
| ------ | ------ | -------- | ------------- | ---------------------------------------------------- |
| filter | string | yes      |               | 筛选项 {'start_date':'', 'end_date':'', 'Media': []} |

返回结果：

```json
Status: 200 OK
{
	'url': 'https://modeanalytics.com/ihandy/reports......',
 }
```

#### 获取当前用户的 view 列表

```http
GET /dashboard/user/roles/<role_id>/views
```

 请求参数：

| Name          | Type   | Required | Default Value | Description |
| ------------- | ------ | -------- | ------------- | ----------- |
| view_category | string | yes      | mode          | view分类    |

返回结果：

```json
Status: 200 OK
{
    "views": [
        {
            "all_dimensions": [
                "Agency Type",
                "Month",
                "Payee",
                "Media",
                "Advertiser Company",
                "Advertiser Department",
                "APP Category",
                "APP Name"
            ],
            "view_category": "mode",
            "view_id": 1,
            "view_name": "Monthly Media Reporting"
        }, ....
    ]
}
```

#### 获取角色 view 列表

在 settings -> roles -> Dashboard views, 获取角色的views

```http
GET /dashboard/roles/<role_id>/views
```

 请求参数：

| Name          | Type   | Required | Default Value | Description |
| ------------- | ------ | -------- | ------------- | ----------- |
| view_category | string | no       | mode          | view 分类   |

返回结果：

```json
Status: 200 OK
{
    "views": [
        {
            "dimensions": [
                {
                    "name": "Agency Type", 
                    "scope": [
                        "outsource"
                    ]
                }, ....
            ], 
            "raw_data": true, 
            "view_id": 4, 
            "view_name": "Account Alert - Unknown Account Payee"
        }, .....
    ]
}

```



#### 查询当前用户某个 view 信息

```http
GET /dashboard/user/roles/<role_id>/views/<view_id>
```

返回结果：

```json
Status: 200 OK
{
    "all_dimensions": [
        "Agency Type", 
        "Month", 
        "Payee", 
        "Media", 
        "Advertiser Company", 
        "Advertiser Department", 
        "APP Category", 
        "APP Name"
    ], 
    "dimensions": [
        {
            "name": "Agency Type", 
            "scope": []
        },....
    ], 
    "raw_data": true, 
    "view_id": "1", 
    "view_name": "Monthly Media Reporting"
}
```

#### 查询角色某个 view 信息

在view的详情页
```http
GET /dashboard/roles/<role_id>/views/<view_id>
```

e.g: https://dev-cp-console.appcloudbox.net/v1/dashboard/user/roles/68/views/1

返回结果：

```json
Status: 200 OK
{
          'view_id':'',
          'view_name':'',
          'raw_data':'',
          'dimensions':[{
              'name':'',
              'scope': []
          },]
 }
```
#### 修改角色某个 view 信息

```http
PUT /dashboard/roles/<role_id>/views/<view_id>
```

 请求参数：

| Name        | Type | Required | Default Value | Description                                                  |
| ----------- | ---- | -------- | ------------- | ------------------------------------------------------------ |
| raw\_data | boolean | yes      | False | 是否可以下载|
| dimensions | json | yes |{}|权限列表：[{"name": "", "scope": []}]|


返回结果：

```json
Status: 200 OK
```

#### 删除角色单个 view

```http
DELETE /dashboard/roles/<role_id>/views/<view_id>
```
返回结果：
```json
Status: 200 OK
```

