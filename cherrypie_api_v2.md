### company

#### 获取公司列表

    GET /companies

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no||排序规则|
|page|int|no|||
|per_page|int|no|||

返回结果：

```json
Status: 200 OK
{
    "companies": [
        { # 参见 CompanyInfo
          "company_id": "",
          "category": ,
          "alias": "",
          "created_by": "",  # 新增时间
          "legal_name": "",
          "status": 1/2,
          "created": "",
        },
        ...
    ]
}
```

##### CompanyInfo

|Name|Type|Values|Description|
|---|---|---|---|
|company_id|int||公司 ID|
|category|int||公司类型：1 为 Internal, 2 为 UA Vendor, 3 为 External_Advertiser, 4 为 Agency|
|alias|string||公司别称|
|created_by|string||公司创建者|
|legal_name|string||公司名称|
|status|int|1 为 enabled, 2 为 disabled|状态|
|created|long||创建时间|

#### 获取公司信息

    GET /companies/<company_id>

返回结果：

    Status: 200 OK
    {# 参见 CompanyInfo
      "company_id": "",
      "category": ,
      "alias": "",
      "legal_name": "",
      "account_admin": "",
      "fraud_settings": {},
      "status": 1/2,
      "created_by": "",  # 新
      "created": "",
    }

#### 添加新公司

    POST /companies

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|alias|string|yes||公司别称|
|legal_name|string|yes||公司名称|

返回结果：

    Status: 200 OK
    {
      "company_id": "",
      "created": "",
    }

#### 修改公司    # 因涉及改动太多，暂不支持修改

    PUT /companies/<company_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|alias|string|yes||公司别称|
|legal_name|string|yes||公司名称|

返回结果：

    Status: 200 OK

#### 更新公司match_name 

    PUT /orgs/<org_id>/companies/<company_id>/match_names

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|match_name|list string|yes|[]|[匹配名称列表|


返回结果：

    Status: 200 OK


### organization

#### 添加新的部门

    POST /orgs

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|category|int|yes||部门类型：1 为 Internal Advertiser，2 为 MB Consulting Team，3 为 MB Agency Team，4 为 UA Department，5 为 Finance|
|name|string|yes||名称|
|superior_org_id|int|no||上级部门 ID|
|company_id|int|yes||公司 ID|
|visibility|list string|no|[]|product team 列表。默认 []，表示所有可见。|
|offer_effective_date_limit|int|no|1|offer 的生效时间是否受限制，1:  受限制，生效时间只能是明天，2: 不受限制，任意时间。|
返回结果：

    Status: 400 Bad Request
    {
        "error": "name is repeated" # 名称重复
    }
    Status: 200 OK # 添加成功
    {
      "org_id": "xxx",
      "created":xxx// 创建时间戳
    }

#### 获取部门列表

    GET /orgs

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no|筛选|
|order_by|string|no|排序规则|
|page|int|no||
|per_page|int|no||

返回结果：

    Status: 200 OK
    {
        "orgs": [
            { # 参见 OrgInfo
              "org_id": "",
              "name": "xxx",
              "category": "xxx",
    		  "company_id": "",
    		  "company_name": "",
    		  "superior_org_name": "",
    		  "superior_org_id": "",
    		  "created_by": "",
              "visibility": [],
              "status": 1/2,
              "offer_effective_date_limit": 1/2,
            },
            ...
        ],
        "page": ,
        "per_page": ,
        "total": ,
    }

#### 获取部门详情

    GET /orgs/<org_id>

返回结果：

    Status: 200 OK
    { # 参见 OrgInfo
      "org_id": "",
      "name": "xxx",
      "category": "xxx",
      "company_id": "",
      "superior_org_id": "",
      "creator": "",
      "visibility": [],
      "status": 1/2,
      "offer_effective_date_limit": 1/2,
    }
#### 修改部门

	PUT /orgs/<org_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|visibility|list string|no|[]|product team 列表。默认 []，表示所有可见。|
|offer_effective_date_limit|int|no|||


#### 存储页面权限

    PUT /page_permissions

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|permissions|json dict|yes||前端自己维护存储格式|

返回结果：

    Status: 200 OK

#### 获取页面权限

    GET /page_permissions

返回结果：

    Status: 200 OK
    {
        "permissions": {}
    }


#### 获取默认功能权限列表

    GET /actions

返回结果：

    Status: 200 OK
    {
        "actions": {}
    }

### role

#### 获取角色列表

    GET /roles

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no|筛选|
|order_by|string|no|排序规则|
|page|int|no||
|per_page|int|no||

返回结果：

    Status: 200 OK
    {
      "roles": [
        {
          "role_id": "",
          "name": "",
          "company_name": "",
    	  "org_name": "",
    	  "org_id": "",
    	  "superior_org_id": "",
    	  "created_by: "","
          "created": ,
        },
        ...
      ],
     "page": ,
     "per_page": ,
     "total": ,
    }

#### 添加角色

    POST /roles

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|name|string|yes||名称|
|company_id|int|no||角色的公司 ID|
|org_id|int|no||角色对应的 组织 ID|

返回结果：

	Status: 200 OK # 添加成功
	{
	  "role_id": "xxx",
	  "created":xxx// 创建时间戳
	}

#### 获取角色详情

    GET /roles/<role_id>

返回结果：

	Status: 200 OK
	{
	  "role_id": "",
	  "name": "",
	  "company_id": "",
	  "org_id": "",
	  "creator: "",
	  "modules: "",
	  "actions: "",
	  "resources: "",
	  "status": "",
	  "updated": "",
	  "created": "",
	}
#### 修改角色

    PUT /roles/<role_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|name|string|yes||名称|

返回结果：

	Status: 200 OK

#### 修改角色权限

    PUT /roles/<role_id>/access

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|modules|json array|no||页面权限列表|
|actions|json array|no||功能权限列表|
|resources|json array|no||通用数据权限列表|

返回结果：

	Status: 200 OK

#### 获取用户列表

```
GET /users
```

请求参数：

| Name      | Type   | Required | Default Value | Description |
| --------- | ------ | -------- | ------------- | ----------- |
| filter_by | string | no       | 筛选          |             |
| order_by  | string | no       | 排序规则      |             |
| page      | int    | no       |               |             |
| per_page  | int    | no       |               |             |
| role_id  | int    | no       | 角色id               |             |

返回结果：

```
Status: 200 OK
{
    "users": [
        {
          "user_id": "",
          "email": "",
          "name": "",
          "roles": [
          { "role_id": "",
            "name": "",
            "company_name": "",
            "company_id": "",
            "superior_org_id": "",
            "org_id": "",
            "org_name": "",
            "org_category": "",
            "modules": "",
            "actions": "",
            "resources": "",
              }
          ],
          "optimizer_id": "",
          "created_by": "",
          "status": 1/2,
          "created": ""
        },
        ...
    ],
    "page": ,
    "per_page": ,
    "total": ,
}
```

####获取登录用户信息

```
GET /user
```

返回结果：

```
Status: 200 OK
{
  "email": "",
  "name": "",
  "roles": [

      { "role_id": "",
        "role_name": "",
        "company_name": "",
        "company_id": "",
        "superior_org_id": "",
        "org_id": "",
        "modules": "",
        "actions": "",
        "resources": "",
        "org_category": "",
        "org_name": "",},
  ],
  "optimizer_id": "",
  "created_by": "",
  "status": 1/2,
  "created": ""
}
```

 

#### 添加用户

    POST /users

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|name|string|yes||用户名|
|email|string|yes||用户邮箱|
|role_ids|json|no||角色 ID|
|optimizer_id|string|no||优化师 ID|

返回结果：

	Status: 200 OK # 添加成功
	{
	  "user_id": "xxx",
	  "created":xxx// 创建时间戳
	}

#### 获取用户详情

    GET /users/<user_id>

返回结果：

	Status: 200 OK
	{
	  "user_id": "",
	  "name": "",
	  "email": "",
	  "optimizer_id": "",
	  "creator: "",
	  "status": "",
	  "updated": "",
	  "created": "",
	}

#### 修改用户

    PUT /users/<user_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|name|string|yes||用户名|
|role_ids|json|no||角色 ID|
|optimizer_id|string|no||优化师 ID|

返回结果：

	Status: 200 OK

#### 停用用户

    PUT /users/<user_id>/disabled

返回结果：

    Status: 200 OK #

#### 启用用户

    PUT /users/<user_id>/enabled

返回结果：

    Status: 200 OK #


#### 将产品 Offer 分配给 用户

    PUT /orgs/<org_id>/offers/<offer_id>/assign/users

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|users|list string|yes||用户列表|

返回结果：

    Status: 200 OK

#### 将产品 分配给 用户

    PUT /orgs/<org_id>/products/<product_id>/assign/users

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|users|list string|yes||用户列表|

返回结果：

    Status: 200 OK

#### 将公司分配给 用户

    PUT /orgs/<org_id>/companies/<company_id>/assign/users

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|users|list string|yes||用户列表|

返回结果：

    Status: 200 OK


### AccountManager

#### 获取ad_account列表

        GET /offer/ad_accounts

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| page  | integer  | no       | 1             | 页号        |
| per_page  | integer  | no       | 10             | 每页条数        |
| order_by  | string  | no       | 无             | 排序规则        |
| filter_by | string  | no       | 无             | 筛选          |

返回结果：

	Status: 200 OK
	{
		'ad_accounts': [
			{
				"agency_type": "opua",
				"media": "facebook",
				"account_id": "614178692097293",
				"account_name": "Domob-Handishiji-1014-01",
				"payee": "papaya",
				"default_payee": "MobileFlame",
				"bank_info": "MobileFlame Limited",
				"credit_card_id": "xxx",
				"updated": 1529743721000,
				"created": 1529743721000,
			},
	   		...
	   ]
	   'total': '',
	   'page': '',
	   'per_page': ''
	}

#### 获取组织下的ad_account 列表

        GET /orgs/<org_id>/manager_accounts/<manager_id>/ad_accounts

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| page  | integer  | no       | 1             | 页号        |
| per_page  | integer  | no       | 10             | 每页条数        |
| order_by  | string  | no       | 无             | 排序规则        |
| filter_by | string  | no       | 无             | 筛选          |
| distinct_by | string  | no       | 无             | distinct          |
| csv_title | string  | no       | 无             | 导出 CSV          |


返回结果：

	Status: 200 OK
	{
		'ad_accounts': [
			{
				"account_id": "614178692097293",
				"account_name": "Domob-Handishiji-1014-01",
				"all_changed_date": {},
				"contract_id": 4,
				"contract_name": "MeetSocial_Facebook",
				"created": 1529743721000,
				"current_changed_date": 1529743721000,
				"last_contract_id": 4,
				"last_contract_name": "MeetSocial_Facebook",
				"manager_id": "1",
				"manager_name": "facebook_mf",
				"media": "facebook",
				"payee": "papaya",
				"account_type": 1,
				"default_payee": "MobileFlame",
				"bank_info": "MobileFlame Limited",
				"source": "opua",
				"credit_card": "1",
				"card_id": "xinyongkade mingzi",
				"status": 1,
				"updated": 1529743721000
			},
	   		...
	   ]
	   'total': '',
	   'page': '',
	   'per_page': ''
	}

#### 单个修改 account

        PUT /orgs/<org_id>/manager_accounts/<manager_id>/ad_accounts

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| account_ids | array  | yes       | 无             | |
| payee | string  | no       | 无             | |
| default_payee | string  | no       | 无             | |
| bank_info | string  | no       | 无             ||
| credit_card | int  | no       | 无             ||
| contract_info_lst | json  | no       | 无             ||
| media | string  | no       | 无             ||

返回结果：

    Status: 200 OK

#### 批量修改 account

        PUT /orgs/<org_id>/manager_accounts/<manager_id>/ad_accounts/batch_changed

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| account_ids | array  | yes       | 无             | |
| payee | string  | no       | 无             | |
| account_type | string  | no       | 无             | |
| default_payee | string  | no       | 无             | |
| bank_info | string  | no       | 无             ||
| credit_card | int  | no       | 无             ||
| contract_info | json array  | no       | 无             ||
| media | string  | no       | 无             ||

返回结果：

    Status: 200 OK


#### Settings 获取 default_payee 列表

        GET /settings/default_payee

返回结果：

    Status: 200 OK
    {
    	default_info: [
    			xxx,
    			xxx
    	]
    }


#### Settings 修改 default_payee 列表

        PUT /settings/default_payee

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| default_payee | array  | yes       | 无             | |

返回结果：

    Status: 200 OK

#### Settings 获取 bank_info 列表

        GET /settings/bank_info

返回结果：

    Status: 200 OK
    {
    	bank_info: [
    			xxx,
    			xxx
    	]
    }


#### Settings 修改 bank_info 列表

        PUT /settings/bank_info

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| bank_info | array  | yes       | 无             | |

返回结果：

    Status: 200 OK

#### 获取 App category 

         GET /settings/app_categories 

返回结果：

    Status: 200 OK
    {
    	app_categories: [
    			    xxx,
    			    xxx
    	]
    }


#### 更新 App category

        PUT /settings/app_categories

请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| app_categories | list string | yes |无 |  |

返回结果：

    Status: 200 OK



