### API

#### 获取BM列表
    GET /orgs/<org_id>/business_managers

返回结果：

    Status: 200 OK
    {
        "business_managers": [
            { 
              "name": "",
              "manager_id": ,
              "timezone": "",
              "status": "",
            },
            ...
        ]
    }
    
#### 获取system user列表

    GET /orgs/<org_id>/system_users

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no||排序规则|
|page|int|no|1|
|per_page|int|no|10|

返回结果：

    Status: 200 OK
    {
        "system_users": [
            { 
              "system_user_id": "",
              "manager_id": ,
              "manager_name": "",
              "name": "",
              "role": "",
              "status": "",
              "created": "",
              "updated": ""
            },
            ...
        ]
    }


#### 获取全量fanpage列表

    GET /fanpages

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no||排序规则|
|page|int|no|1|
|per_page|int|no|10|

返回结果：

    Status: 200 OK
    {
        "fanpages": [
            { 
              "page_id": "",
              "name": ,
              "category": "",
              "link": "",
              "status": "",
              "created": "",
              "updated": ""
            },
            ...
        ]
    }

    
#### 获取fanpage列表

    GET /orgs/<org_id>/fanpages

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no||排序规则|
|page|int|no|1|
|per_page|int|no|10|

返回结果：

    Status: 200 OK
    {
        "fanpages": [
            { 
              "page_id": "",
              "name": ,
              "category": "",
              "link": "",
              "status": "",
              "created": "",
              "updated": ""
            },
            ...
        ]
    }

#### 获取facebook user列表

    GET /orgs/<org_id>/facebook_users

请求参数：
 
|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no||排序规则|
|page|int|no|1||
|per_page|int|no|10||

返回结果：

    Status: 200 OK
    {
        "facebook_users": [
            { 
              "facebook_user_id": "",
              "user_id": ,
              "name": "",
              "token": "",
              "email": "",
              "status": "",
              "created": "",
              "updated": ""
            },
            ...
        ]
    }
    
#### 更新facebook user的token

    PUT /orgs/<org_id>/facebook_users
 
 请求参数：
    
|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|token|string|yes||facebook账户的短期token|

返回结果：

    Status: 200 OK
        
#### 获取facebook user详情

    GET /orgs/<org_id>/facebook_users/<facebook_user_id>

返回结果：

    Status: 200 OK
    
    { 
        "facebook_user_id": "",
        "user_id": ,
        "facebook_name": "",
        "facebook_email": "",
        "status": "",
        "created": "",
        "updated": ""
    }
    
#### 从api获取accounts
        
	GET /facebook_api/ad_accounts

 请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|facebook_user_id|string|yes|||
	
返回结果:
	
	Status: 200 OK
    {
        "accounts": [
            { 
              "account_id": "",
              "name": "",
              "timezone": "",
              "status": "",
            },
            ...
        ]
    }

#### 获取account账户列表
        
	GET /orgs/<org_id>/ad_accounts

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no||排序规则|
|page|int|no|1|
|per_page|int|no|10|
	
返回结果:
	
	Status: 200 OK
    {
        "accounts": [
            {
            "account_id": "", 
            "account_name": "", 
            "all_changed_date": "", 
            "created": "", 
            "current_changed_date": "", 
            "manager_id": "", 
            "media": "", 
            "product_num": "", 
            "status": "", 
            "updated": "",
            "extra": {
                       "timezone": "",
                       "currency": "",
                       "disable_reason": ""
                     }

        },
            ...
        ]
    }
        
#### facebook_user 批量绑定 account

    PUT /orgs/<org_id>/facebook_users/<facebook_user_id>/ad_accounts
 
 请求参数：
    
|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|account_ids|json|yes||账号id列表|

返回结果：

    Status: 200 OK

#### facebook_user 绑定单个 account

    PUT /orgs/<org_id>/facebook_users/<facebook_user_id>/ad_accounts/<ad_account_id>/connected
 

返回结果：

    Status: 200 OK

#### facebook_user 解绑单个 account

    PUT /orgs/<org_id>/facebook_users/<facebook_user_id>/ad_accounts/<ad_account_id>/disconnected
 
返回结果：

    Status: 200 OK


#### 获取product详情

	GET /orgs/<org_id>/products/<product_id>
	
返回结果：

    Status: 200 OK
	{
        "fanpages": [
            { 
              "page_id": "",
              "name": ,
              "category": "",
              "link": "",
              "status": "",
              "created": "",
              "updated": ""
            },
            ...
        ],
		"product_id": "",
		"org_id": "",
		"company_id": "",
		"company_name": "",
		"company_category": "",
		"internal_name":"",
		"store": "",
		"product_type":"",
		"bundle_id":"",
		"apple_id":"",
		"store_link": "",
		"support_device": "",
		"min_os_version": "",
		"appsflyer_id": "",
		"facebook_id": "",
		"facebook_fanpage": "",
		"default_page_id": "",
		"users": "",
		"status": "",
		"updated": "",
		"created": ""
		}

#### product 绑定 page

	PUT /orgs/<org_id>/products/<product_id>/fanpages
	
请求参数：
    
|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|fanpage_ids|json|yes||粉丝页id列表|
|default_page_id|string|yes||默认的粉丝页id|

返回结果：

    Status: 200 OK

### Model

#### `UserOfFacebook`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|facebook_user_id|varchar(50)|主键，fb账号下的user_id|yes|yes|no|
|user_id|interger|cherrypie系统中的user_id|no|yes|no|
|name|varchar(50)|fb中的用户名|no|yes|no|
|email|varchar(50)|fb中绑定的邮箱|no|yes|no|
|token|text|fb用户的token|yes|yes|no|
|status|integer|token的有效状态，1、为有效，2、为无效|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `FacebookUserAccountMap`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|facebook_user_id|varchar(50)|主键|no|yes|no|
|account_id|varchar(50)|主键|no|yes|no|
|status|interger|绑定状态 1、Active 2、Lost|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `UserOfSystem`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|system_user_id|varchar(50)|主键|yes|yes|no|
|manager_id|interger|manager的编号|no|yes|no|
|name|varchar(50)|system user的用户名|no|yes|no|
|role|varchar(50)| EMPLOYEE或者ADMIN，用户的身份|no|yes|no|
|status|interger|system user状态 1、Active 2、Lost|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `SystemUserAccountMap`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|system_user_id|varchar(50)|主键|no|yes|no|
|account_id|varchar(50)|主键|no|yes|no|
|status|interger|绑定状态 1、Active 2、Lost|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `Fanpage`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|page_id|varchar(50)|主键|yes|yes|no|
|name|varchar(50)|主页名称|no|yes|no|
|category|varchar(50)|页面类型|no|yes|no|
|link|varchar(100)|页面网址|no|no|no|
|verification_status|varchar(50)|核实状态|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `ManagerAdAccount` (修改)

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|account_id|varchar(100)|广告账户 id|no|yes|no|
|manager_id|varchar(100)|manager 编号|no|yes|no|
|media|varchar(32)|media|no|yes|no|
|status|integer|广告账户状态：1 为 正常 enable； 2 为 封户 disable 3 为未绑定 unbinding| no|yes|no|
|current_changed_date|datetime|状态改变更新时间|no|yes|no|
|all_changed_date|list dict|状态改变 [{date, (status1, status2)}]|no|yes|no|
|account_name|varchar(100)||no|no|yes|
|last_contract_id|interger||no|no|yes|
|last_contract_name|varchar(100)||no|no|yes|
|extra|json|{"disable_reason": "", "currency": "", "timezone": ""}(新增)|no|no|yes|
|updated|datetime|更新时间|no|no|no|
|created|datetime|创建时间|no|yes|no|

#### `ProductAccountMap`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|product_id|interger|主键|no|yes|no|
|account_id|varchar(50)|主键|no|yes|no|
|status|interger|绑定状态 1、Active 2、Lost|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `ProductPageMap`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|product_id|interger|主键|no|yes|no|
|page_id|varchar(50)|主键|no|yes|no|
|status|interger|page状态 1、默认 2、非默认|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `FacebookUserPageMap`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|facebook_user_id|varchar(50)|主键|no|yes|no|
|page_id|varchar(50)|主键|no|yes|no|
|status|interger|page状态 1、默认 2、非默认|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|












	
	
    

    
    
	
