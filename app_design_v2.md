### API

#### 从data home获取APP信息
```http
GET /datahome/applications/<internal_name>
```
请求参数:
|Name|Type|Required|Description|
|-|-|-|
|internal\_name|string|yes|APP 的名字|


#### 获取产品列表

```http
GET /products
```

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter\_by|string|no||筛选|
|order\_by|string|no|排序规则|
|page|int|no||
|per\_page|int|no||
|columns|string|no|字段筛选|
|q|string|no|正则匹配internal name|

eg: /v1/products?columns=internal\_name,company.alias,company.category

返回结果：

```json
Status: 200 OK
{
    "page": 1,
    "per_page": 1,
    "products": [
        {
            "apple_id": null,
            "appsflyer_id": null,
            "bundle_id": "com.daily.horoscope.plus",
            "company": {}, 
            "company_id": 1,
            "created": 1520579403000,
            "default_page_id": "278932119108288",
            "facebook_fanpage": "dailyhoroplus",
            "facebook_id": "676424012550459",
            "fanpage": {}, 
            "internal_name": "Fortune_A",
            "min_os_version": null,
            "org": {}, 
            "org_id": 5,
            "product_id": 1,
            "product_type": "Lifestyle",
            "status": 1,
            "store": 1,
            "store_link": "https://play.google.com/store/apps/details?id=com.daily.horoscope.plus",
            "support_device": "Phone",
            "updated": 1541221796000,
            "users": [], 
        }
    ],
    "total": 95
}
```


#### 部门与产品
##### 获取部门下的产品
```http
GET /orgs/<org_id>/products
```

##### 给部门新增产品
```http
POST /orgs/<org_id>/products
```

表单:

|Name|Type|Required|Description|
|-|-|-|-|
|internal\_name|string|yes|名字|
|company\_id|int|yes|公司ID|
|store|int|yes|应用商店: 1为Google play, 2为App store|
|product\_type|string|yes|应用类型|
|store\_link|string|yes|应用商店的链接|
|bundle\_id|string|yes|包的名字|
|apple\_id|string|no|App store 上的id|
|support\_device|string|no|支持的设备, 如"Phone"|
|min\_os\_version|string|no|兼容的最低操作系统版本|
|appsflyer\_id|string|no||
|facebook\_id|string|no|facebook app id|
|facebook\_fanpage|string|no|粉丝页|

#### 单个产品

##### 获取单个产品的信息

```http
GET /orgs/<org_id>/products/<product_id>
```

响应: fanpages, list of fanpages' info.

```json
{
    "apple_id": null,
    "appsflyer_id": null,
    "bundle_id": "com.daily.horoscope.plus",
    "company_id": 1,
    "created": 1520579403000,
    "default_page_id": "278932119108288",
    "facebook_fanpage": "dailyhoroplus",
    "facebook_id": "676424012550459",
    "fanpages": [],
    "internal_name": "Fortune_A",
    "min_os_version": null,
    "org_id": 5,
    "product_id": 1,
    "product_type": "Lifestyle",
    "status": 1,
    "store": 1,
    "store_link": "https://play.google.com/store/apps/details?id=com.daily.horoscope.plus",
    "support_device": "Phone",
    "updated": 1541221796000,
    "users": [
        {}
    ]
}
```



##### 修改单个APP的信息

```http
PUT /orgs/<org_id>/products/<product_id>
```

请求表单: (同上表单)

| Name             | Type | Required | Description |
| ---------------- | ---- | -------- | ----------- |
| store            |      |          |             |
| product_type     |      |          |             |
| store_link       |      |          |             |
| apple_id         |      |          |             |
| support_device   |      |          |             |
| min_os_version   |      |          |             |
| appsflyer_id     |      |          |             |
| facebook_id      |      |          |             |
| facebook_fanpage |      |          |             |

#### 给产品分配user

```http
PUT /orgs/<org_id>/products/<product_id>/assign/users
```

| Name  | Type | Required | Description       |
| ----- | ---- | -------- | ----------------- |
| users | list | yes      | list of users' id |

#### 给用户分配facebook粉丝页

```http
PUT /orgs/<org_id>/products/<product_id>/fanpages
```

请求表单:

| Name             | Type   | Required | Description          |
| ---------------- | ------ | -------- | -------------------- |
| fanpage_ids      | string | no       |                      |
| default_fange_id | string | yes      | 链接的 facebook 主页 |

#### 启用/停用 产品(软删除)

```http
PUT /orgs/<org_id>/products/<product_id>/<operation>
```

