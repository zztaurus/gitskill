#### 账户授权API设计

##### 获取BM列表
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
    
##### 获取system user列表

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


##### 获取全量fanpage列表

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

    
##### 获取fanpage列表

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

##### 获取facebook user列表

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
    
##### 更新facebook user的token

    PUT /orgs/<org_id>/facebook_users
 
 请求参数：
    
|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|token|string|yes||facebook账户的短期token|

返回结果：

    Status: 200 OK
        
##### 获取facebook user详情

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
    
##### 从api获取accounts
        
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

##### 获取account账户列表
        
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
        
##### facebook_user 绑定 account

    PUT /orgs/<org_id>/facebook_users/<facebook_user_id>/ad_accounts
 
 请求参数：
    
|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|account_ids|json|yes||账号id列表|

返回结果：

    Status: 200 OK


##### 获取product详情

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

##### product 绑定 page

	PUT /orgs/<org_id>/products/<product_id>/fanpages
	
请求参数：
    
|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|fanpage_ids|json|yes||粉丝页id列表|
|default_page_id|string|yes||默认的粉丝页id|

返回结果：

    Status: 200 OK

	
	
    

    
    
	
