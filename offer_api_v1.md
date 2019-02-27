## 说明

group_by 规则：共分为两个区域，两个区域用“|”分隔，前面的是聚合的条件，后面的是聚合的方式是求和还是求平均值，格式例子如下：

group:date, app_id,country|sum:installs;sum:retention_day_1

order_by 规则：多个排序字段按先后顺序用'|'分隔
排序格式如下：sort_name:sort_rule，其中 sort_rule 可以为 0（降序）和 1（升序）
filter_by 规则：多个筛选条件用`|`分隔，筛选条件为`or`的时候使用`,`分隔，筛选关键字与筛选值之间使用`: 关系词：`表示

关系词如下：

|关系词|意思|是否必须|例子|
|---|---|---|---|
|`$eq`| 筛选关键字对应内容等于筛选值 |no|`field_name:$eq:field_value` 或者 `field_name:field_value`（省略时只加一个`:`)|
|`$gt`| 筛选关键字对应内容大于筛选值 |no|`field_name:$gt:field_value`|
|`$gte`| 筛选关键字对应内容大于等于筛选值 |no|`field_name:$gte:field_value`|
|`$lt`| 筛选关键字对应内容小于筛选值 |no|`field_name:$lt:field_value`|
|`$lte`| 筛选关键字对应内容小于等于筛选值 |no|`field_name:$lte:field_value`|
|`$exists`| 筛选关键字对应内容包含筛选值（完全匹配） |yes|`field_name:$exists:field_value`|
|$ne| 筛选关键字对应内容不等于筛选值 |yes|field_name:$ne:field_value|
|$contains| 筛选关键字对应内容包含筛选值（不完全匹配）|yes|field_name:$contains:field_value|
|$be|  此项是否为空|yes|increases:$be:yes 或者 decreases:$be:yes|
|$like| 模糊匹配 |yes|name:$like:nihao|

格式如下：

    field_name1:field_value1|field_name2:field_value2,field_name3:field_value3|
    field_name4:$exists:field_value4,field_name5:$exists:field_value5
    field_name6:$ne:field_value6,field_name7:$ne:field_value7

示例：/v1/orgs?filter_by=category:1,2,3|org_id:1&order_by=created:0

## dock_console
无

## dock_offer
### assign
#### 给某个用户分配产品

    PUT /orgs/<org_id>/users/<email>/assign/products

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|product_ids|list |yes||产品 ID 列表|

返回结果：

    Status: 200 OK  # 分配成功

#### 给某个用户分配公司

    PUT /orgs/<org_id>/users/<email>/assign/companies

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|company_ids|list int|yes||公司 ID 列表|

返回结果：

    Status: 200 OK  # 分配成功

#### 将产品 Offer 分配给 business_development

    PUT /orgs/<org_id>/offers/<offer_id>/assign/business_development

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|business_development|list string|yes||邮箱地址列表|

返回结果：

    Status: 200 OK

#### 将产品 Offer 分配给 optimizers

    PUT /orgs/<org_id>/offers/<offer_id>/assign/optimizers

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|optimizers|list string|yes||邮箱地址列表|

返回结果：

    Status: 200 OK

#### 将产品 Offer 分配给某个公司

    PUT /orgs/<org_id>/offers/<offer_id>/assign/companies

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|company_ids|list int|yes||公司 ID 列表|

返回结果：

    Status: 200 OK

### audittrail

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

### company

#### 获取 vendor 列表外部接口

    GET /offer/vendors

返回结果：

    Status: 200 OK
    {
        "vendors": [
            { # 参见 CompanyInfo
              "company_id": "",
              "category": ,
              "alias": "",
              "legal_name": "",
              "business_development": [],
              "account_manager": [],
              "status": 1/2,
              "created": "",
            },
            ...
        ]
    }

#### 获取 vendor 详细信息外部接口

    GET /offer/vendors/<alias>

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
      "bank_info": '',
      "status": 1/2,
      "created": "",
      "media_config": [{}],
      "vendor_account": [{}],
    }

#### 获取公司列表

    GET /orgs/<org_id>/companies

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no|排序规则|
|category|int|yes||
|page|int|no||
|per_page|int|no||

返回结果：

    Status: 200 OK
    {
        "companies": [
            { # 参见 CompanyInfo
              "company_id": "",
              "category": ,
              "alias": "",
              "legal_name": "",
              "business_development": [],
              "account_manager": [],
              "status": 1/2,
              "created": "",
            },
            ...
        ]
    }

##### CompanyInfo

|Name|Type|Values|Description|
|---|---|---|---|
|company_id|int||公司 ID|
|category|int||公司类型：1 为 Internal, 2 为 UA Vendor, 3 为 External_Advertiser, 4 为 Agency|
|alias|string||公司别称|
|legal_name|string||公司名称|
|company_managers|list||公司列表|
|status|int|1 为 enabled, 2 为 disabled|状态|
|operators|list string|delete|操作列表|
|created|long||创建时间|

#### 获取公司信息

    GET /orgs/<org_id>/companies/<company_id>

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

#### 添加新公司

    POST /orgs/<org_id>/companies

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|category|int|yes||公司类型：1 为 internal, 2 为 UA Vendor, 3 为 External_Advertiser, 4 为 Agency|
|alias|string|yes||公司别称|
|legal_name|string|yes||公司名称|
|bank_info|string|no|||

返回结果：

    Status: 200 OK
    {
      "company_id": "",
      "created": "",
    }


#### 修改公司 fraud_settings

    PUT /orgs/<org_id>/companies/<company_id>/fraud_settings

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|fraud_settings|FraudSettings|||防欺诈设置，category 为 2 时必填|


fraud_settings

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|click_flood_cti|int|yes|||
|dynamic_discount|int|yes|||
|hijacking_ctd|int|yes|||
|hijacking_cti|int|yes|||
|postback|string|yes|||
|postback_status|int|||状态：1 为 enabled,2 为 disabled|

返回结果：

    Status: 200 OK

#### 修改公司 admin_settings

    PUT /orgs/<org_id>/companies/<company_id>/admin_settings

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|account_admin|email|||admin 邮箱地址，category 为 2 时必填|

返回结果：

    Status: 200 OK

#### 修改公司 bank_info

    PUT /orgs/<org_id>/companies/<company_id>/bank_info

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|bank_info|string|||category 为 2 时必填|

返回结果：

    Status: 200 OK

##### MediaConfig

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|media|string|yes|||
|agency|string|yes|||
|media_source|string|yes|||


##### VendorAccount

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|media|string|yes|||
|account_id|string|yes|||

#### 获取 vendor_account (account_setting) 列表

    GET /orgs/<org_id>/companies/<company_id>/vendor_account

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no|排序规则|
|distinct_by|string|no||
|page|int|no||
|per_page|int|no||

返回结果：

    Status: 200 OK
    {
        "vendor_account": [
            {
              "payee": "",
              "media": ,
              "account_id": "",
            },
            ...
        ]
    }


#### 新增 vendor_account(account_setting) 列表

    POST /orgs/<org_id>/companies/<company_id>/vendor_account

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|vendor_account|list VendorAccount(dict)|no||vendor 账户|

##### VendorAccount

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|media|string|yes|||
|account_id|string|yes|||


返回结果：

    Status: 200 OK

#### 修改 单个 vendor_account(account_setting)

    PUT /orgs/<org_id>/companies/<company_id>/vendor_account/<media_account_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|account_id|string|yes|---|---|
|media|-string|yes|---|---|


返回结果：

    Status: 200 OK

#### 删除 单个 vendor_account(account_setting) 列表

    DELETE /orgs/<org_id>/companies/<company_id>/vendor_account/<media_account_id>

请求参数：

无

返回结果：

    Status: 200 OK

#### 获取 media_config 列表

    GET /orgs/<org_id>/companies/<company_id>/media_config

请求参数：

无

返回结果：

    Status: 200 OK
    {
        "media_config": [
            {
              "payee": "",
              "media": ,
              "media_source": "",
            },
            ...
        ]
    }

#### 修改与新建 media_config 列表

    PUT /orgs/<org_id>/companies/<company_id>/media_config

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|media_config|list MediaConfig|yes||media 的配置|

##### MediaConfig

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|media|string|yes|||
|agency|string|yes|||
|media_source|string|yes|||

返回结果：

    Status: 200 OK




#### 给公司的管理员发送密码邮件

    POST /orgs/<org_id>/companies/<company_id>/password

#### 启用公司

    PUT /companies/<company_id>/enabled

返回结果：

    Status: 200 OK # 启用成功

#### 停用公司

    PUT /companies/<company_id>/disabled

返回结果：

    Status: 200 OK # 停用成功

### group
#### 创建 Region 组

    POST /orgs/<org_id>/region_groups

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|name|string|yes||组名称|
|regions|list string|yes||列表|

返回结果：

    Status: 200 OK
    {
      "region_group_id": "",
      "created": ""
    }

#### 获取 Region 组列表

    GET /orgs/<org_id>/region_groups

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
      "region_groups": [
      {
    	"region_group_id": "",
    	"name": "",
    	"regions": [],
    	"created": ""
      },
      ...
      ]
    }
#### 删除 RegionGroup 列表

    DELETE 	/orgs/<org_id>/region_groups/<region_group_id>

返回结果：
    Status: 200 OK

### offer
#### 获取组织的 Offer 列表

    GET /orgs/<org_id>/offers

 请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer|no|1|页号|
|per_page|integer|no|10|每页条数|
|order_by|string|no|排序规则|
|filter_by|string|no||筛选|
|distinct_by|string|no||distinct_by 不为空，page 和 per_page 参数失效|

请求示例：

    GET /orgs/1/offers?order_by=offer_type:1|product_name:0&page=1&per_page=10
    GET /orgs/1/offers?filter_by=org_name:085

返回结果：

    Status: 200 OK
    [#返回结果为 list，每个元素均为 Offer 中 distict_by 名称对应的值
      ...
    ]
    Status: 200 OK
    {
        "offers": [
            { # 参见 OfferInfo
              "offer_id": "",
              "offer_type": 1/2，
              "product_id": "",
              "product_name": "",
              "product_info": {...},
              "org_id": "",
              "org_name": "",
              "org_category": ,
              "company_id": "",
              "company_name": "",
              "company_category": ,
              "consumer_org_id": "",
              "consumer_org_name": "",
              "consumer_org_category": ,
              "consumer_company_id": "",
              "consumer_company_name": "",
              "consumer_company_category": ,
              "optimizers": [],
              "media": [],
              "effective_date": "",
    		  "notes": {
    				"text": "",
    				"pictures": [
    					{"file_name": "",
    					"file_type": "",
    					"url": ""},
    				]
    			  },
              "current_version": "",
              "version_status": ,
              "status": "",
              "updated": "",
              "created": "",
            },
            ...
        ],
        "page": ,
        "per_page": ,
        "total": ,
    }

#### 获取组织的 Offer 详情

    GET /orgs/<org_id>/offers/<offer_id>

返回结果：

    Status: 200 OK
    { # 参见 OfferInfo
      "offer_id": "",
      "offer_type": 1/2，
      "product_id": "",
      "product_name": "",
      "product_info": {...},
      "org_id": "",
      "org_name": "",
      "org_category": ,
      "company_id": "",
      "company_name": "",
      "company_category": ,
      "consumer_org_id": "",
      "consumer_org_name": "",
      "consumer_org_category": ,
      "consumer_company_id": "",
      "consumer_company_name": "",
      "consumer_company_category": ,
      "optimizers": [],
      "media": [],
      "effective_date": "",
      "notes": {
    		"text": "",
    		"pictures": [
    			{"file_name": "",
    			"file_type": "",
    			"url": ""},
    		]
    	  },
      "current_version": "",
      "last_version": { # 参见 OfferVersionInfo},
      "status": "",
      "updated": "",
      "created": "",
      "items": [
          {# 参见 OfferItemInfo
    		"regions": [],
    		"languages": [],
    		"daily_budget": {},
    		"daily_install": {},
    		"daily_cpi": {},
    		"kpi_by_retention": {},
    	  },
          ...
      ]
    }

#### 获取组织的 Offer 版本信息

    GET /orgs/<org_id>/offers/<offer_id>/versions

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
      "versions": [
        { # 参见 OfferVersionInfo
          "offer_type": 1/2，
      	   "product_id": "",
          "product_name": "",
          "product_info": {...},
          "org_id": "",
          "org_name": "",
          "org_category": ,
          "company_id": "",
          "company_name": "",
          "company_category": ,
          "consumer_org_id": "",
          "consumer_org_name": "",
          "consumer_org_category": ,
          "consumer_company_id": "",
          "consumer_company_name": "",
          "consumer_company_category": ,
          "media": [],
          "effective_date": "",
    	  "notes": {
    		  "text": "",
    		  "pictures": [
    		  {"file_name": "",
    		  "file_type": "",
    			  "url": ""},
    		  ]
    	  },
          "current_version": "",
          "version_status": "",
          "updated": "",
          "created": "",
          "items": [
            {# 参见 OfferItemInfo
    	    	"regions": [],
    		   "languages": [],
    		   "daily_budget": {},
    		   "daily_install": {},
    		   "daily_cpi": {},
    		   "kpi_by_retention": {},
    	    },
            ...
          ]
        },
        ...
      ],
      "page": ,
     "per_page": ,
     "total": ,
    }

##### ItemInfo

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|regions|list string|yes||国家简码列表|
|languages|list string|no||语言列表|
|daily_budget|DailyBudgetInfo|no||每日花销范围|
|daily_install|DailyInstallInfo|no||每日安装量目标范围|
|daily_cpi|json format: {"9000_": "0.95", "0_3000": "0.85", "3000_9000": "0.90"}|no||阶梯价|
|kpi_by_retention|json format: {"50_100": "1", "0_45": "0", "45_50": "auto"}|no||阶梯 kpi|

#### 创建产品 Offer

    POST /orgs/<org_id>/offers

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|items|ItemInfo|yes||item 信息列表|
|organization_id|string|yes||产品投放的组织 ID|
|offer_type|int|yes||类型：1 为 task,2 为 order|
|product_id|string|yes||所属产品 ID|
|media|list string|yes||投放平台列表：facebook,adwords|
|effective_date|string|yes|生效日期："yyyy-mm-dd"|
|notes||json formart: {"text": "", "pictures": [{"file_name": "","file_type": "","url":""}]}|yes|说明|

##### DailyBudgetInfo

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|min|double|no||区间最小值|
|max|double|no||区间最大值|

DailyInstallInfo

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|min|int|no||区间最小值|
|max|int|no||区间最大值|

返回结果：

    Status: 200 OK
    {
      "offer_id": "",
      "created": "",
    }

#### 修改产品 Offer

    PUT /orgs/<org_id>/offers/<offer_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|offer_type|int|yes||类型：1 为 task,2 为 order|
|effective_date|string|yes|生效日期："yyyy-mm-dd"|
|notes||json formart: {"text": "", "pictures": [{"file_name": "", "file_type": "", "url":""}]}|yes|说明|
|items|ItemInfo|yes||item 信息列表|
|organization_id|string|no||产品投放的组织 ID，只有第一个版本在编辑状态前才可修改|
|product_id|string|no||产品 ID，只有第一个版本在编辑状态前才可修改|

返回结果：

    Status: 200 OK

#### 提交产品 Offer 的新版本申请

    PUT /orgs/<org_id>/offers/<offer_id>/submit

返回结果：

    Status: 200 OK

#### 审核产品 Offer 新版本

    PUT /orgs/<org_id>/offers/<offer_id>/review

返回结果：

    Status: 200 OK

#### 通过产品 Offer 新版本

    PUT /orgs/<org_id>/offers/<offer_id>/passed

返回结果：

    Status: 200 OK

#### 拒绝产品 Offer 新版本

    PUT /orgs/<org_id>/offers/<offer_id>/rejected

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|category|int|yes|拒绝原因类型：1 为 expired。|
|reason|string|no|拒绝原因说明|

返回结果：

    Status: 200 OK

#### 提交产品 Offer 当前版本停止申请

    PUT /orgs/<org_id>/offers/<offer_id>/stopped_submit

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|expiration_date|string|yes|截止日期："yyyy-mm-dd"|

返回结果：

    Status: 200 OK

#### 审核产品 Offer 当前版本停止申请

    PUT /orgs/<org_id>/offers/<offer_id>/stopped_review

返回结果：

    Status: 200 OK

#### 通过产品 Offer 当前版本停止申请

    PUT /orgs/<org_id>/offers/<offer_id>/stopped_passed

返回结果：

    Status: 200 OK

#### 拒绝产品 Offer 当前版本停止申请

    PUT /orgs/<org_id>/offers/<offer_id>/stopped_rejected

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|category|int|yes|拒绝原因类型：1 为 expired。|
|reason|string|no|拒绝原因说明|

返回结果：

    Status: 200 OK

#### 取消产品 Offer 当前版本 Coming Stoped 状态，恢复其运行

    PUT /orgs/<org_id>/offers/<offer_id>/stopped_canceled

返回结果：

    Status: 200 OK

#### offer 上传图片

	POST /orgs/<org_id>/offer_files
请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|file|File|yes||文件流|
|file_name|str|no||自定义文件名|


返回结果：

    Status: 200 OK
    {
      "file_name": "",
      "file_type": "",
      "url": "http://xxxx"
    }

### organization

#### 添加新的组织

    POST /orgs

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|category|int|yes||组织类型：1 为 Internal Advertiser，2 为 MB Consulting Team，3 为 MB Agency Team，4 为 UA Department，5 为 Finance|
|name|string|yes||名称|
|default_leader|string|yes||默认 leader 邮箱地址|
|company_id|int|no||名称|
|visibility|list string|no|[]|product team 列表。默认 []，表示所有可见。|
|functions|list string|no||组织可见的功能列表。|
|offer_effective_date_limit|int|yes|1|offer 的生效时间是否受限制，1:  受限制，生效时间只能是明天，2: 不受限制，任意时间。|
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

#### 获取组织列表

    GET /orgs
    GET /auth/orgs # 获取已授权的组织

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no|筛选|
|order_by|string|no|排序规则|
|category||yes||
|page|int|no||
|per_page|int|no||

返回结果：

    Status: 200 OK
    {
        "orgs": [
            { # 参见 OrgInfo
              "org_id": "",
              "name": "xxx",
              "company_alias": "xxx",
              "default_leader": "xxx",
              "visibility": [],
              "status": 1/2,
              "operators": ["modify", "delete"],
              "offer_effective_date_limit": 1/2,
              "functions": ["Offer",],
            },
            ...
        ],
        "page": ,
        "per_page": ,
        "total": ,
    }

#### 修改组织

	PUT /orgs/<org_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|name|varchar|yes||名称|
|default_leader|varchar|yes||默认邮箱地址|
|visibility|list string|no|[]|product team 列表。默认 []，表示所有可见。|
|functions|list string|no||组织可见的功能列表。|
|offer_effective_date_limit|int|no|||

返回结果：

    Status: 200 OK

#### 停用组织

    PUT /orgs/<org_id>/disabled

返回结果：

	Status: 403 Forbidden # 没有权限
	Status: 200 OK # 停用成功

#### 启用组织

    PUT /orgs/<org_id>/enabled

返回结果：

	Status: 403 Forbidden # 没有权限
	Status: 200 OK # 启用成功

### product

#### 获取产品列表外部接口

    GET /offer/products

返回结果：

    Status: 200 OK
    {
        "products": [
            { # 参见 ProductInfo
              "product_id": "",
              "org_id": '''',
              "company_id": "",
              "company_category": ,
              "internal_name": "",
              "store": 1/2,
              "bundle_id": "",
              "apple_id": "",
              "store_link": "",
              "support_device": "",
              "min_os_version": "",
              "appsflyer_id": "",
              "facebook_id": "",
              "appsflyer_id": "",
              "fackbook_fanpage": "",
              "product_manager": "",
              "status": "",
              "updated": "",
              "created": "",
              "running_offer_count": ,
            },
            ...
        ],
    }


#### 获取单个产品信息外部接口

    GET /offer/products/<internal_name>

返回结果：

    Status: 200 OK
    { # 参见 ProductInfo
      "product_id": "",
      "org_id": '''',
      "company_id": "",
      "company_category": ,
      "internal_name": "",
      "store": 1/2,
      "bundle_id": "",
      "apple_id": "",
      "store_link": "",
      "support_device": "",
      "min_os_version": "",
      "appsflyer_id": "",
      "facebook_id": "",
      "appsflyer_id": "",
      "fackbook_fanpage": "",
      "product_manager": "",
      "status": "",
      "updated": "",
      "created": "",
      "running_offer_count": ,
    }

#### 获取产品列表

    GET /orgs/<org_id>/products

   请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no|筛选|
|order_by|string|no|排序规则|
|category||yes||
|page|int|no||
|per_page|int|no||
|q|string|no||关键字查询|

返回结果：

    Status: 200 OK
    {
        "products": [
            { # 参见 ProductInfo
              "product_id": "",
              "org_id": '''',
              "company_id": "",
              "company_category": ,
              "internal_name": "",
              "store": 1/2,
              "bundle_id": "",
              "apple_id": "",
              "store_link": "",
              "support_device": "",
              "min_os_version": "",
              "appsflyer_id": "",
              "facebook_id": "",
              "appsflyer_id": "",
              "fackbook_fanpage": "",
              "product_manager": "",
              "status": "",
              "updated": "",
              "created": "",
              "running_offer_count": ,
            },
            ...
        ],
        "page": ,
        "per_page": ,
        "total": ,
    }

#### 创建产品

    POST /orgs/<org_id>/products

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|internal_name|string|yes|产品名称|
|company_id|int|yes||公司 ID|
|store|integer|yes||商店类型：1 为 GooglyPlay，2 为 AppStore|
|store_link|string|yes||应用商店链接|
|bundle_id|string|no||android 包名称|
|apple_id|string|no||ios 包 id|
|support_device|string|yes||支持设备|
|min_os_version|string|yes||最小系统版本支持|
|appsflyer_id|string|yes||appsflyer 的 ID|
|facebook_id|string|yes||facebook 的 ID|
|facebook_fanpage|string|yes||facebook 的 Page|

返回结果：

    Status: 200 OK
    {
      "product_id": "",
      "internal_name": "",
      "created": "",
    }

#### 更新产品

    PUT /orgs/<org_id>/products/<product_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|store|integer|yes||商店类型：1 为 GooglyPlay，2 为 AppStore|
|bundle_id|string|no||android 包名称|
|apple_id|string|no||ios 包 id|
|store_link|string|yes||应用商店链接|
|support_device|string|yes||支持设备|
|min_os_version|string|yes||最小系统版本支持|
|appsflyer_id|string|yes||appsflyer 的 ID|
|facebook_id|string|yes||facebook 的 ID|
|facebook_fanpage|string|yes||facebook 的 Page|

返回结果：

    Status: 200 OK

#### 停用产品

    PUT /orgs/<org_id>/products/<product_id>/disabled

返回结果：

    Status: 200 OK

#### 启用产品

    PUT  /orgs/<org_id>/products/<product_id>/enabled

返回结果：

    Status: 200 OK


### reporting
#### 获取报表列表

    GET /orgs/<org_id>/reports

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer|no|1|页号|
|per_page|integer|no|10|每页条数|
|order_by|string|no|排序规则|
|filter_by|string|no||筛选|
|distinct_by|string|no||distinct_by 不为空，page 和 per_page 参数失效|
|csv_title|list|no||导出的 CSV 的表头|

请求示例：

    GET /orgs/<org_id>/reports?distinct_by=org_name:085
    GET /orgs/<org_id>/reports

返回结果：

    Status: 200 OK
    [#返回结果为 list，每个元素均为 Reporting 中 distict_by 名称对应的值
        ...
    ]

    Status: 200 OK
    {
      "reports": [
    	{ # 参见 ReportInfo
    	  "report_id": "",
    	  "item_id": "",
    	  "item_name": "",
    	  "offer_id": "",
    	  "offer_type": 1/2,
    	  "offer_media": "",
    	  "product_id": "",
    	  "product_name": "",
    	  "org_id": "",
    	  "org_name": "",
    	  "company_id": "",
    	  "company_name": "",
    	  "company_category": "",
    	  "summary": xx,
    	  "status": "",
    	  "status_info": {},
    	  "supporting": [],
    	  "updated": "",
    	  "created": "",
        },
    	...
    ],
    "page": ,
    "per_page": ,
    "total": ,
    }

#### 获取报表详情

    GET /orgs/<org_id>/reports/<report_id>

返回结果：

    Status: 200 OK
    { # 参见 ReportInfo
      "item_id": "",
      "report_month": "",
      "item_name": "",
      "offer_id": "",
      "offer_type": "",
      "offer_media": "",
      "product_id": "",
      "product_name": "",
      "org_id": "",
      "org_name": "",
      "company_id": "",
      "company_name": "",
      "company_category": "",
      "increases": [{ # 参见 Increase
        "name": "",
        "summary": "",
      }...],
      "decreases": [{ # 参见 Decrease
        "name": "",
        "summary": "",
      }...],
      "summary": xx,
      "status": "",
      "status_info": [{ # 参见 StatusInfo
        "created": "",
        "email": "",
        "action": "",
        "comment": ""
      }...],
      "supporting": [{ # 参见 SupporInfo
        "name": "",
        "url": "",
      }...],
      "updated": "",
      "created": "",
    }

StatusInfo

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|created|string|yes||创建时间|
|email|string|yes||邮箱地址|
|action|string|yes||动作|
|comment|string|yes||评论|

#### 获取报表基础数据

    GET /orgs/<org_id>/reports/<report_id>/records

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
      "records":[
        { # 参见 ReportDataInfo
          "create_date": "",
          "product_name": "",
          "media": "",
          "country": "",
          "install": ,
          "optimizer": "",
          "impression": ,
          "click": ,
          "spent": ,
          "purchase": ,
          "ctr": ,
          "cvr": ,
          "ppi": ,
          "cpi": ,
          "cpm": ,
          "created": xx,
      },
      ...
    ],
    "page": ,
    "per_page": ,
    "total": ,
  }

#### 获取报表基础留存数据

    GET /orgs/<org_id>/reports/<report_id>/retentions

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
      "records":[
        { # 参见 ReportRetentionInfo
          "create_date": "",
          "product_name": "",
          "media": "",
          "country": "",
          "install": ,
          "retention_day_1": ,
          "retention_install": ,
      },
      ...
    ],
    "page": ,
    "per_page": ,
    "total": ,
  }


#### 上传报表文件

    POST /orgs/<org_id>//reports/<report_id>/files

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|file|File|yes||文件流|

返回结果：

    Status: 200 OK
    {
      "file_name": "",
      "file_type": "",
      "url": "http://xxxx"
    }

#### 添加报表依赖信息

    POST /orgs/<org_id>/reports/<report_id>/extra

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|increases|list Increase|no||添加项|
|decreases|list Decrease|no||删减项|
|supporting|list SupportInfo|no||说明|

Increase/Decrease

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|name|string|yes||名称|
|summary|decimal|yes||总价|

SupportInfo

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|file_name|string|yes||文件名称|
|file_type|string|yes||文件类型|
|url|Url|yes||文件路径|

返回结果：

    Status: 200 OK

 #### 提交待审核的报表

    PUT /orgs/<org_id>/reports/<report_id>/submit

返回结果：

    Status: 200 OK

#### review 报表

    PUT /orgs/<org_id>/reports/<report_id>/review

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|comment|string|no||备注|

返回结果：

    Status: 200 OK

#### 再次 review 报表

    PUT /orgs/<org_id>/reports/<report_id>/review2

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|comment|string|no||备注|

返回结果：

    Status: 200 OK

#### review 通过报表

    PUT /orgs/<org_id>/reports/<report_id>/passed

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|comment|string|yes||备注|

返回结果：

    Status: 200 OK

#### review 拒绝报表

    PUT /orgs/<org_id>/reports/<report_id>/rejected

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|comment|string|yes||备注|

返回结果：

    Status: 200 OK

### settings
#### 设置自动结算日期

    PUT /settings/reporting_day

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|reporting_day|integer|yes||自动结算日期，可选项从 1 到 28|

返回结果：

	Status: 200 OK # 设置成功

#### 获取自动结算日期

    GET /settings/reporting_day

返回结果：

	Status: 200 OK # 设置成功
	{"reporting_day": 8}

#### 设置 opua_medias

    PUT /settings/opua_medias

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|opua_medias|string|yes||各 media 之间用逗号区分，"facebook,search ads,adwords"|

返回结果：

	Status: 200 OK # 设置成功

#### 获取 opua_medias

    GET /settings/opua_medias

返回结果：

	{"opua_medias": "facebook,search ads, adwords"}


#### 设置 outsource_medias

    PUT /settings/outsource_medias

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|outsource_medias|string|yes||各 media 之间用逗号区分，"facebook,adwords"|


返回结果：

	Status: 200 OK # 设置成功

#### 获取 outsource_medias

    GET /settings/outsource_medias

返回结果：
	{"outsource_medias": "facebook,adwords"}

### todo
#### 获得 ToDo 列表

        GET /todo

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
      "todo":[
        {
          "todo_id": "",
          "title": "",
          "status": 1/2,
          "created": "",
              "updated":""
         },
         ...
       ],
       "page": ,
       "per_page": ,
       "total": ,
       "unread_total":,
     }

#### 获得 ToDo 详情

        GET /todo/<todo_id>

返回结果：

    Status: 200 OK
    {
        "todo_id": "",
        "email":"",
        "message":"",
        "title": "",
        "status": 1/2,
        "created": "",
        "updated":""
      }

#### 更新 ToDo 列表状态

        PUT /todo/<todo_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|status|integer|yes|1|是否已读 1 为未读，2 为已读|

返回结果：

    Status: 200 OK

#### 修改所有未读 TODO 为已读状态

        PUT /todo/clear

返回结果：

    Status: 200 OK

### userole

#### 获取角色列表

    GET /orgs/org_id/roles

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
          "description": "",
          "created": ,
        },
        ...
      ],
    }

#### 向组织添加角色

    POST /orgs/<org_id>/roles

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|email|string|yes||名称|
|role_id|int|yes||角色列表对应的 id：Leader，Viewer，Product Manager，Account Manager|

返回结果：

	Status: 200 OK # 添加成功

#### 获取用户列表

    GET /orgs/org_id/users

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no|筛选|
|order_by|string|no|排序规则|
|page|int|no||
|per_page|int|no||
|q|string|no||关键字查询|

返回结果：

    Status: 200 OK
    {
        "users": [
            { # 参见 UserInfo
              "email": "",
              "status": 1/2,
              "operators": ["delete"],
            },
            ...
        ],
        "page": ,
        "per_page": ,
        "total": ,
    }

##### UserInfo

|Name|Type|Values|Description|
|---|---|---|---|
|email|string||邮箱地址|
|role_id|string||角色 ID|
|is_default|boolean||是否是 default|
|status|int|1 为 enabled, 2 为 disabled|状态|
|operators|list string|delete|操作列表|

#### 获取登录用户的信息

    GET /orgs/<org_id>/users

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no|筛选|
|order_by|string|no|排序规则|
|page|int|no||
|per_page|int|no||
|q|string|no|关键字查询|

返回结果：

	Status: 200 OK #
	{
	  "user": {
	    "email": "",
	    "role_id": xxx,
	    "is_default: true/false,
	    "status": 1/2,
	  }
	}

#### 停用用户

    PUT /orgs/<org_id>/users/<email>/disabled

返回结果：

    Status: 200 OK #

#### 启用用户

    PUT /orgs/<org_id>/users/<email>/enabled

返回结果：

    Status: 200 OK #

#### 获取管理员列表

    GET /orgs/org_id/admins

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
        "admins": [
            { # 参见 UserInfo
              "email": "",
              "status": 1/2,
              "operators": ["delete"],
            },
            ...
        ],
        "page": ,
        "per_page": ,
        "total": ,
    }

#### 添加新的管理员

    POST /orgs/org_id/admins

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|email|string|yes||名称|


返回结果：

    Status: 400 Bad Request
    {
        "error": "email is not valid" # email 不合法
    }
    Status: 200 OK # 添加成功
    {
      "email": "xx@ihandysoft.com",
      "created":xxx// 创建时间戳
    }

#### 停用管理员

    PUT /orgs/org_id/admins/<email>/disabled

返回结果：

	Status: 403 Forbidden # 没有权限
	Status: 200 OK # 删除成功

#### 启用管理员

    PUT /orgs/org_id/admins/<email>/enabled

返回结果：

	Status: 403 Forbidden # 没有权限
	Status: 200 OK # 删除成功

### Optimizer

#### 获取优化师组列表

    GET /orgs/<org_id>/optimizer_groups

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
      "optimizer_groups": [
      {
    	"group_id": "",
    	"org_id": "",
    	"name": "",
    	"department_id": "",
    	"status": ""
    	"created": ""
    	"updated": ""
      },
      ...
      ]
    }

#### 创建优化师组

    POST /orgs/<org_id>/optimizer_groups

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|name|string|yes||组名称|
|optimizers|list(optimizer_id)|no|||
|leader|optimizer_id|no|||

返回结果：

    Status: 200 OK
    {
      "optimizer_group_id": "",
      "created": ""
    }

#### 获取单个优化师组信息

    GET /orgs/<org_id>/optimizer_groups/<optimizer_group_id>

返回结果：

    Status: 200 OK
    {
      "group_id": "",
      "org_id": "",
      "name": "",
      "department_leader": "",
      "status": "",
      "created": "",
      "updated": "",
      "optimizers": []
    }

#### 修改单个优化师组信息

    PUT /orgs/<org_id>/optimizer_groups/<optimizer_group_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|name|string|no||组名称|
|leader|string|no||组名称|
|optimizers|list(optimizer_id)|yes|||

返回结果：

    Status: 200 OK

#### 删除优化师组

    DELETE /orgs/<org_id>/optimizer_groups/<optimizer_group_id>

返回结果：

    Status: 200 OK

#### 获取优化师列表

        GET /orgs/<org_id>/optimizers

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
       'optimizers':[
            {
              "optimizer_id": "",
              "org_id":"",
              "email":"",
              "status": ,
              "updated": ,
              "created": ,
            }
       ]
       'page': ,
       'per_page': ,
       'total':
    }

#### 添加（创建）优化师

        POST /orgs/<org_id>/optimizers

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|optimizer_id|string|yes|no||
|group_name|string|no|no||
|email|string|no|no|邮箱|

返回结果：

    Status: 200 OK
    {
       'optimizer_id':'',
       'org_id':''
       'email':'',
       'status':'',
    }

#### 修改优化师信息

        PUT /orgs/<org_id>/optimizers/<optimizer_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|email|string|no|no|邮箱|

返回结果：

    Status: 200 OK
    {
       'optimizer_id':'',
       'org_id':''
       'email':'',
       'status':'',
    }

#### 启用优化师

    PUT /orgs/<org_id>/optimizers<optimizer_id>/enabled

返回结果：

    Status: 200 OK # 启用成功

#### 停用优化师

    PUT /orgs/<org_id>/optimizers<optimizer_id>/disabled

返回结果：

    Status: 200 OK # 停用成功

#### 修改优化师组所属的部门

    PUT /orgs/<org_id>/optimizers/departments

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|department_leader|string|yes|no|邮箱|
|group_list|list(group_name)|yes|no|组名字|

返回结果：

    Status: 200 OK # 停用成功

### datahome

#### 获取 App 信息

    GET /datahome/applications/<internal_name>

返回结果：

    Status: 400 BadRequest {"error_message": "internal name is not valid"}
    Status: 200 OK
    {
      "primary_id": "",
      "basic_status": "",
      "basic_isolate_status": "",
      "basic_app_status": "",
      "basic_url_schema": "",
      "basic_appgroup": "",
      "basic_hs_appid": "",
      "basic_app_name": "",
      "basic_internal_name": "",
      "basic_project_group": "",
      "basic_app_platform": "",
      "basic_system_name": "",
      "store_ios_online_category": "",
      "store_ios_apple_id": "",
      "store_ios_bundle_id": "",
      "marketing_facebook_id": "",
      "marketing_facebook_fanpage": "",
      "analytic_google_analytics_id": "",
      "analytic_flurry_id": "",
      "store_android_online_category": "",
      "store_android_package_name": "",
      "create_time": "",
      "update_time": "",
    }

### Account

#### 登录

    POST /accounts/login

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|username|string|yes||账号|
|password|string|yes||密码|

返回结果：

    Status: 400 BadRequest {"error_message": "username or password is not valid"}
    Status: 200 OK 登录成功

#### 重置密码

    POST /accounts/password/reset

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|password|string|yes||密码|
|new_password|string|yes||新密码|

返回结果：

    Status: 400 BadRequest {"error_message": "password is not valid"}
    Status: 200 OK 重置成功

### Retetion

#### 获取 retention 列表信息

    GET /retentions

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|date_span|string|yes||日期区间，格式："2018-01-01,2018-02-01"|
|product_id|string|no||产品 ID|
|media_sources|list string|no||媒体源 列表|
|site_ids|list string|no||站点 ID 列表|
|regions|list string|no||国家列表|
|distinct_by|string|no||regions 为 country|
|events|string|no||事件列表|
|group_by|string|no||聚合字段|


返回结果：

    Status: 200 OK
    {
      "records": [
        {
          "install_day": "",
          "app_id":"",
          "product_name": "",
          "site_id": "",
          "media_source": "",
          "region": "",
          "install": ,
          "satisfy":,
          "retention_day_1": ,
          "origin_retention":"" ,
          "output_retention":"" ,
        },
      ],
      "total": ,
    }

### 结算

#### 获取结算数据

    GET /v1/offer/reporting

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|date_span|string|yes||日期区间，格式："2018-01-01,2018-01-31"，包含开始日期和截止日期|
|app_name|string|yes||产品内部名称|
|source|string|yes||结算类型，可选值有：opua（内部单）, outsource（外部单）|

返回结果：

    Status 400  #系统内没有该产品的 offer 信息
    {
      "error_message": "app_name is not configured"
    }

    Status: 200 OK
    {
      "items": [
        {
          "source": "",
          "create_date": "",
          "product_name": "",
          "app_id": "",
          "media": [],
          "regions": [],
          "payer": "",
          "payee": "",
          "installs": ,
          "purchase": ,
          "daily_cpi": {},
        },
      ],
    }

#### 获取投放团队的优化师列表

    GET /v1/offer/optimizers

返回结果：

    Status: 200 OK
    {
      "optimizers": [
        {
          "optimizer_id": "",
          "email": "",
          "company": "",
          "payee": "",
        },
      ],
    }

#### 获取 offer version 版本历史

    GET /v1/offer/versions

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|date_span|string|yes||日期区间，格式："2018-01-01,2018-01-31"，包含开始日期和截止日期|
|app_name|string|yes||产品内部名称|

返回结果：

    Status 400  #系统内没有该产品的 offer 信息
    {
      "error_message": "app_name is not configured"
    }

    Status: 200 OK
    {
      "versions": [
        { # 参见 OfferVersionInfo
          "offer_type": 1/2，
      	   "product_id": "",
          "product_name": "",
          "product_info": {...},
          "org_id": "",
          "org_name": "",
          "org_category": ,
          "company_id": "",
          "company_name": "",
          "company_category": ,
          "consumer_org_id": "",
          "consumer_org_name": "",
          "consumer_org_category": ,
          "consumer_company_id": "",
          "consumer_company_name": "",
          "consumer_company_category": ,
          "media": [],
          "effective_date": "",
    	  "notes": {
    		  "text": "",
    		  "pictures": [
    		  {"file_name": "",
    		  "file_type": "",
    			  "url": ""},
    		  ]
    	  },
          "current_version": "",
          "version_status": "",
          "updated": "",
          "created": "",
          "items": [
            {# 参见 OfferItemInfo
    	    	"regions": [],
    		   "languages": [],
    		   "daily_budget": {},
    		   "daily_install": {},
    		   "daily_cpi": {},
    		   "kpi_by_retention": {},
    	    },
            ...
          ]
        },
        ...
      ],
    }

#### 隐藏指定的 offer

```
PUT /orgs/<org_id>/offers_hide
```

请求参数：

| Name      | Type        | Required | Default Value | Description            |
| --------- | ----------- | -------- | ------------- | ---------------------- |
| offer_ids | list string | yes      |               | 需要隐藏的 offer id 列表 |

请求示例：

```
PUT /orgs/1/offers_hide
```

返回结果：

```
Status: 200 OK
```

#### 取消隐藏指定的 offer

```
PUT /orgs/<org_id>/offers_unhide
```

请求参数：

| Name      | Type        | Required | Default Value | Description            |
| --------- | ----------- | -------- | ------------- | ---------------------- |
| offer_ids | list string | yes      |               | 取消隐藏的 offer id 列表 |

请求示例：

```
PUT /orgs/1/offers_unhide
```

返回结果：

```
Status: 200 OK
```
#### 更新 s3 中的 ua 相关配置文件

	POST /orgs/<org_id>/ua_config/<file_id>
请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|file|File|yes||文件流|


返回结果：

    Status: 200 OK


#### 获取 s3 中 ua 相关配置文件

	GET /orgs/<org_id>/ua_config/<file_id>

返回结果：

    Status: 200 OK
	文件流数据
