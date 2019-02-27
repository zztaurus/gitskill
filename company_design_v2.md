### API


#### 获取公司列表

```http
GET /companies
```

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by_fields|string|no||筛选字段和值|
|order_by_fields|string|no|排序规则|
|columns|string|no|None|列.子列|
|page|int|no|||
|per_page|int|no|||

返回结果：

```json
Status: 200 OK
{
"companies": [
    {  # 参见 CompanyInfo
        "account_admin": "",
        "alias": "testLoading2",
        "bank_info": "",
        "buying_side": null,
        "category": 1,
        "company_id": 165,
        "created": 1539932396000,
        "created_by": "youdeng.lu",
        "creator": "114",
        "legal_name": "testLoading2",
        "match_name": null,
        "status": 1,
        "updated": 1539932396000,
        "users": []
    }, ....
],
"page": 1,
"per_page": 10,
"total": 16
}
```

#### 新增公司信息

```http
POST /companies
```

表单

| Name       | Type   | Required | Description  |
| ---------- | ------ | -------- | ------------ |
| alias      | string | yes      | 公司名称缩写 |
| legal_name | string | yes      | 公司法名     |

##### CompanyInfo

获取公司信息

```http
GET /companies/<company_id>
```

|Name|Type|Values|Description|
|---|---|---|---|
|company_id|int||公司 ID|
|category|int||公司类型：1 为 Internal, 2 为 UA Vendor, 3 为 External_Advertiser, 4 为 Agency， 5为media|
|alias|string||公司别称|
|legal_name|string||公司名称|
|status|int|1 为 enabled, 2 为 disabled|状态|
|operators|list string|delete|操作列表|
|created|long||创建时间, 时间戳乘以1000|
|account_admin|string||(deprecated)|
|bank_info|string|||
|buying_side|int|1 - Advertiser<br />2 - Media_buy|区分广告主和优化师团队|
|match_name|list|list of strings|抓取时使用的名字|
|creator|json| dict                              |创建者的to_json|
|updated|long||更新时间, 时间戳乘以1000|
|users|list|list of dict||

#### 获取部门下的公司列表

```http
GET /orgs/<org_id>/companies
```

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by_fields|string|no||筛选|
|order_by_fields|string|no|排序规则|排序规则|
|category|int|yes||分类|
|columns|string|no|               |要求返回的列.子列|
|page|int|no|||
|per_page|int|no|||

返回结果：

```json
Status: 200 OK
{
"companies": [
    {  # 参见 CompanyInfo
        "account_admin": "",
        "alias": "testLoading2",
        "bank_info": "",
        "buying_side": null,
        "category": 1,
        "company_id": 165,
        "created": 1539932396000,
        "created_by": "youdeng.lu",
        "creator": "114",
        "legal_name": "testLoading2",
        "match_name": null,
        "status": 1,
        "updated": 1539932396000,
        "users": []
    }, ....
],
"page": 1,
"per_page": 10,
"total": 16
}
```


#### 获取公司信息

```http
GET /orgs/<org_id>/companies/<company_id>
```

返回结果：

    Status: 200 OK
    {# 参见 CompanyInfo
      "company_id": "",
      "category": ,
      "alias": "",
      "legal_name": "",
      "business_development": [],
      "account_manager": [],
      "media_config": [],
      "account_admin": "",
      "fraud_settings": {},
      "status": 1/2,
      "created": "",
    }

#### 更新公司信息

```http
PUT /orgs/<org_id>/companies/<company_id>
```

表单：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|alias|string|yes||公司别称|

返回结果：

```json
Status: 200 OK
""
```


#### 修改公司 admin_settings(depreacated)

```http
PUT /orgs/<org_id>/companies/<company_id>/admin_settings
```

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|account_admin|email|||admin 邮箱地址，category 为 2 时必填|

返回结果：

```json
Status: 200 OK
""
```

#### 修改公司 bank_info

    PUT /orgs/<org_id>/companies/<company_id>/bank_info

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|bank_info|string|||category 为 2 时必填|

返回结果：

```json
Status: 200 OK
""
```


#### 将用户分配给公司

```http
PUT /orgs/<org_id>/companies/<company_id>/assign/users
```

更新company的users字段, 同时更新user-resources 的关系

请求参数

| Name  | Type   | Required | Description      |
| ----- | ------ | -------- | ---------------- |
| users | string | yes      | list of user ids |

#### 更新公司的match name

```http
PUT /orgs/<org_id>/companies/<company_id>/match_names
```

请求参数:

| Name       | Type           | Required | Description |
| ---------- | -------------- | -------- | ----------- |
| match_name | string or list | yes      |             |


#### 公司的支付信息
##### 获取支付信息列表
```http
GET /orgs/<org_id>/companies/<company_id>/payment_infos
```
请求参数:
|Name	| Type		| Required | Description |
|-|-|-|-|
|page|int|yes| 第几页|
|per_page|int|yes|每页多少个|
|order_by|dict|no|根据什么字段排序|
|filter_by|dict|no|筛选符合条件的数据|
|columns|string|no|只返回列或者子列|
##### 新增支付方式
```http
POST /orgs/<org_id>/companies/<company_id>/payment_infos
```
表单:
|Name|Type|Required|Description|
|-|-|-|
|config\_name|string||
|currency_type|string||
|application_description|string||
|payee|string||
|due_bank|string||
|swift_code|string||
|bank_account|string||
|bank_address|string||
|inward_prompt|string|
|external_prompt|string||
|credit_tearm|string||
|contract_status|int||
|special_approver|string||

##### 更新支付方式
```http
PUT /orgs/<org_id>/companies/<company_id>/payment_infos/<payment_id>
```
表单:
|Name|Type|Required|Description|
|-|-|-|
|currency\_type|string||
|application\_description|string||
|payee|string||
|due\_bank|string||
|swift\_code|string||
|bank\_account|string||
|bank\_address|string||
|inward\_prompt|string|
|external\_prompt|string||
|credit\_tearm|string||
|contract\_status|int||
|special\_approver|string||

