### API

#### 获取产品的有效VersionItem列表

    GET /products/<product_id>/version_items

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|from|string|yes||开始日期|
|to|string|yes||截止日期|
|agency_type|string|yes||投放类型|

返回结果：

    Status: 200 OK
    {
        "items": [
            { # 参见 VersionItemInfo
              ...
            },
            ...
        ]
    }

##### VersionItemInfo

|Name|Type|Values|Description|
|---|---|---|---|


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



Model

#### Offer

| field                     | type                   | description                                                  | unique | index | NULL |      |
| ------------------------- | ---------------------- | ------------------------------------------------------------ | ------ | ----- | ---- | ---- |
| offer_id                  | varchar(10)            | 主键                                                         | yes    | yes   | no   |      |
| offer_type                | integer                | 分类：1 代表 task,2 代表 order                               | no     | yes   | no   |      |
| product_id                | integer                | 产品 ID                                                      | no     | yes   | no   |      |
| product_name              | varchar(50)            | 产品内部名称                                                 | no     | yes   | no   |      |
| product_info              | json                   | 产品信息                                                     | no     | no    | no   |      |
| org_id                    | integer                | 组织 ID                                                      | no     | yes   | no   |      |
| org_name                  | varchar(50)            | 组织名称                                                     | no     | yes   | no   |      |
| org_category              | integer                | 组织类型                                                     | no     | no    | no   |      |
| company_id                | integer                | 公司 ID                                                      | no     | yes   | yes  |      |
| company_name              | varchar(50)            | 公司名称                                                     | no     | yes   | yes  |      |
| company_category          | integer                | 公司类型：1 为 internal, 2 为 UA Vendor, 3 为 External Advertiser | no     | yes   | yes  |      |
| consumer_org_id           | integer                | 产品投放的组织 ID                                            | no     | yes   | no   |      |
| consumer_org_name         | varchar(50)            | 产品投放的组织名称                                           | no     | yes   | no   |      |
| consumer_org_category     | integer                | 组织类型                                                     | no     | no    | no   |      |
| consumer_company_id       | integer                | 产品投放的公司 ID                                            | no     | yes   | yes  |      |
| consumer_company_name     | varchar(50)            | 产品投放的公司名称                                           | no     | yes   | yes  |      |
| consumer_company_category | integer                | 产品投放的公司类型：1 为 internal                            | no     | yes   | yes  |      |
| users                     | json list email        |                                                              | no     | no    | yes  |      |
| version_status            | integer                |                                                              | no     | yes   | yes  |      |
| media                     | json array string      | 投放平台列表                                                 | no     | no    | no   |      |
| sub_media                 | json array string json | 投放平台列表                                                 | no     | no    | no   |      |
| effective_date            | date                   | 生效日期                                                     | no     | yes   | no   |      |
| expiration_date           | date                   | 截止日期                                                     | no     | no    | yes  |      |
| notes                     | json dict              | 说明                                                         | no     | no    | no   |      |
| items                     | json array dict        |                                                              | no     | no    | yes  |      |
| status                    | integer                | 状态：1 为 Running,2 为 Stopped                              | no     | yes   | no   |      |
| current_version           | integer                | 当前版本                                                     | no     | no    | yes  |      |
| updated                   | datetime               | 更新时间                                                     | no     | yes   | no   |      |
| created                   | datetime               | 创建时间                                                     | no     | yes   | no   |      |

#### OfferVersion

| field                  | type             | description                                                  | unique | index | NULL |      |
| ---------------------- | ---------------- | ------------------------------------------------------------ | ------ | ----- | ---- | ---- |
| offer_id               | varchar(10)      | offer 的 ID，和 offer_version 组成联合主键                   | no     | yes   | no   |      |
| offer_version          | integer          | offer 的版本                                                 | no     | yes   | no   |      |
| offer_type             | integer          | 分类：1 代表 task,2 代表 order                               | no     | yes   | no   |      |
| source                 | varchar(10)      | 渠道：opua,outsource                                         | no     | yes   | no   |      |
| product_id             | integer          | 产品 ID                                                      | no     | yes   | no   |      |
| product_name           | varchar(50)      | 产品内部名称                                                 | no     | yes   | no   |      |
| product_info           | json             | 产品信息                                                     | no     | no    | no   |      |
| media                  | list string json | 投放平台列表                                                 | no     | no    | no   |      |
| sub_media              | list string json | 投放平台列表                                                 | no     | no    | no   |      |
| effective_date         | date             | 生效日期                                                     | no     | no    | no   |      |
| expiration_date        | date             | 截止日期                                                     | no     | no    | yes  |      |
| expect_expiration_date | date             | 期望截止日期                                                 | no     | no    | yes  |      |
| notes                  | json dict        | 说明                                                         | no     | no    | no   |      |
| items                  | json array dict  |                                                              | no     | no    | yes  |      |
| status                 | integer          | 状态：1 为 Created,2 为 PendingLeaderReview,3 为 PendingProductTeamReview,4 为 Enabled,5 为 Rejected | no     | yes   | no   |      |
| extra                  | json dict        |                                                              | no     | no    | yes  |      |
| updated                | datetime         | 更新时间                                                     | no     | yes   | no   |      |
| created                | datetime         | 创建时间                                                     | no     | yes   | no   |      |

