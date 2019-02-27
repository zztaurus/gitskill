账户管理设计方案

#### 获取 ManagerAccount 列表

        GET /orgs/<org_id>/manager_accounts

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| order_by  | string  | no       | 无             | 排序规则        |
| filter_by | string  | no       | 无             | 筛选          |


返回结果：

    Status: 200 OK
    {
    	'manager_accounts': [
    		{'manager_id':'',
           'org_id':'',
           'name':'',
    		 'media':'',
    		 'updated':'',
    		 'created':'',
          },
       		...
       ]
       'total': ''
    }

#### 获取 AdAccount 列表

        GET /orgs/<org_id>/manager_accounts/<manager_id>/ad_accounts

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| page      | integer | no       | 1             | 页号          |
| per_page  | integer | no       | 10            | 每页条数       |
| order_by  | string  | no       | 无             | 排序规则      |
| filter_by | string  | no       | 无             | 筛选          |

返回结果：

    Status: 200 OK
    {
    	'ad_accounts': [
    		{'manager_id':'',
       	 'account_id':'',
       	 'media':'',
       	 'companies':[{}],
           'contacts':[{}],
    		 'current_changed_date':'',
           'updated': "",
           'created': "",
         },
         ...
       ]
       'total': ''
       'page': ''
       'per_page': ''
    }

#### 获取 AdAccount 条目的 contract 列表

####  修改 AdAccount 条目的 account_name
        PUT  /orgs/<org_id>/manager_accounts/<manager_id>/ad_accounts/<account_id>

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
|account_name      | string |yes       | no            |账户名称         |


返回结果：

    Status: 200 OK

#### 批量修改 AdAccount 条目

        POST /orgs/<org_id>/manager_accounts/<manager_id>/ad_accounts

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| account_ids | json array | yes  |              | 账户编号的列表 |
| contract_info_list  | json array | no       |             | 合同信息列表       |

返回结果：

    Status: 200 OK


对外付款 api 设计

### agency_settlement

#### 添加对代理的付款单

	POST /orgs/<org_id>/agency_settlements

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|settle_month|string |yes|||
|company_id|string |yes||公司 ID|
|notes| json formart: {"text": "", "pictures": [{"file_name": "","file_type": "","url":""}]}|yes|||
|media|string |yes||投放平台|

返回结果：

	Status: 200 OK
	{
		"created": "",
		"settle_id": ""
	}

#### 提交对代理的付款单审核申请

	PUT /orgs/<org_id>/agency_settlements/<settle_id>/submitted

返回结果：

	Status: 200 OK

#### 审核对代理的付款单

	PUT /orgs/<org_id>/agency_settlements/<settle_id>/reviewed

返回结果：

	Status: 200 OK

#### 通过对代理的付款单

	PUT /orgs/<org_id>/agency_settlements/<settle_id>/passed

返回结果：

	Status: 200 OK

#### 拒绝对代理的付款单

	PUT /orgs/<org_id>/agency_settlements/<settle_id>/rejected

返回结果：

	Status: 200 OK

#### 查询对代理的付款单列表

	GET /orgs/<org_id>/agency_settlements

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer |no|1|页号|
|per_page|integer |no|10|每页条数|
|filter_by|string |no||筛选|
|order_by|string |no||排序规则|

返回结果：

	Status: 200 OK
	{
		"settlements": [
			{
				"settle_id": "",
				"settle_month": ""，
				"media": "",
				"company_id": "",
				"company_name": "",
				"status": "",
				"notes": "",
				"total": "",
				"amount": "",
				"created": "",
				"updated": "",
			},
		...
		],
		"page": ,
		"per_page": ,
		"total": ,
	}

#### 查询对代理的付款单详情

	GET /orgs/<org_id>/agency_settlements/<settle_id>

返回结果：

	Status: 200 OK
	{
		"settle_id": "",
		"settle_month": ""，
		"media": "",
		"company_id": "",
		"company_name": "",
		"status": "",
		"notes": "",
		"total": "",
		"amount": "",
		"created": "",
		"updated": ""
	}

#### 修改对代理付款单

	PUT /orgs/<org_id>/agency_settlements/<settle_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|notes| json formart: {"text": "", "pictures": [{"file_name": "","file_type": "","url":""}]}|yes|||

返回结果：

	Status: 200 OK

#### 获取 account 维度的 agency_settlement 列表

	GET /orgs/<org_id>/agency_settlements/<settle_id>/ad_accounts

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer |no|1|页号|
|per_page|integer |no|10|每页条数|
|filter_by|string |no||筛选|
|order_by|string |no||排序规则|

返回结果：

	Status: 200 OK
	{
		"accounts": [
			{
				"settle_account_id": 1,
                        "account_id": "",
		      	"status": "",
		      	"total": "",
		      	"summary": "",
				"increases": [{ # 参见 Increase
			        "name": "",
			        "summary": "",
			      }...],
			    "decreases": [{ # 参见 Decrease
			        "name": "",
			        "summary": "",
			      }...],
		      	"created": "",
		      	"updated": ""
			},
		...
		],
		"page": ,
		"per_page": ,
		"total": ,
	}

#### 添加 account 维度的 agency_settlement 核减信息

	PUT /orgs/<org_id>/agency_account_settlements/<settle_account_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|increases| json list Increase|no||添加项|
|decreases| json list Dectease|no||删减项|

Increase/Decrease

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|name|string|yes||名称|
|summary|decimal|yes||总价|

返回结果：

	Status: 200 OK

#### agency_settlement 上传图片

	POST /orgs/<org_id>/agency_settlements/files

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|file| File |yes||文件流|
|file_name| str|no||自定义文件名|

返回结果：

	Status: 200 OK
	{
		"file_name": "",
		"file_type": "",
		"url": "http://xxxxx"
	}

### external_settlement/vendor_settlement

#### 添加对外付款单

	POST /orgs/<org_id>/[external|vendor]_settlements

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|settle_month|string |yes|||
|company_id|string |yes||公司 ID|
|consumer_org_id |string |yes||
|notes| json formart: {"text": "", "pictures": [{"file_name": "","file_type": "","url":""}]}|yes|||
|total|string |yes||对外付款总金额|

返回结果：

	Status: 200 OK
	{
		"settle_id": "",
		"created": ""
	}

#### 修改对外付款单

	PUT /orgs/<org_id>/[external|vendor]_settlements/<settle_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|settle_month|string |yes|||
|company_id|string |yes||公司 ID|
|notes| json formart: {pictures": [{"file_name": "","file_type": "","url":""}]}|yes|||
|total|string |yes||对外付款总金额|

返回结果：

	Status: 200 OK

#### external_settlements/vendor_settlement 上传图片

	POST /orgs/<org_id>/[external|vendor]_settlements/files

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|file| File |yes||文件流|
|file_name| str|no||自定义文件名|

返回结果：

	Status: 200 OK
	{
		"file_name": "",
		"file_type": "",
		"url": "http://xxxxx"
	}

#### 查询对外付款单列表

	GET /orgs/<org_id>/[external|vendor]_settlements

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer |no|1|页号|
|per_page|integer |no|10|每页条数|
|filter_by|string |no||筛选|
|order_by|string |no||排序规则|

返回结果：

	Status: 200 OK
	{
		"settlements": [
			{
				"settle_id": "",
				"settle_month": ""，
				"company_id": "",
				"company_name": "",
				"status": "",
				"notes": "",
				"total": "",
				"created": "",
				"updated": "",
			},
		...
		],
		"page": ,
		"per_page": ,
		"total": ,
	}

#### 查询对外付款单详情

	GET /orgs/<org_id>/[external|vendor]_settlements/<settle_id>

返回结果：

	Status: 200 OK
	{

		"settle_id": "",
		"settle_month": ""，
		"company_id": "",
		"company_name": "",
		"status": "",
		"notes": "",
		"total": "",
		"created": "",
		"updated": "",
	}

#### 提交对外付款单

	PUT /orgs/<org_id>/[external|vendor]_settlements/<settle_id>/submitted1

返回结果：

	Status: 200 OK

#### 确认对外付款单

	PUT /orgs/<org_id>/[external|vendor]_settlements/<settle_id>/reviewed1

返回结果：

	Status: 200 OK

#### 提交 invoice 后的账单

	PUT /orgs/<org_id>/[external|vendor]_settlements/<settle_id>/submitted2

返回结果：

	Status: 200 OK

#### 审核对外付款单

	PUT /orgs/<org_id>/[external|vendor]_settlements/<settle_id>/reviewed2

返回结果：

	Status: 200 OK

#### 再次审核对外付款单（external 对外付款多出一个 review 环节）

	PUT /orgs/<org_id>/external_settlements/<settle_id>/reviewed3

返回结果：

	Status: 200 OK

#### 通过对外付款单

	PUT /orgs/<org_id>/[external|vendor]_settlements/<settle_id>/passed

返回结果：

	Status: 200 OK

#### 拒绝对外付款单

	PUT /orgs/<org_id>/[external|vendor]_settlements/<settle_id>/rejected

返回结果：

	Status: 200 OK


### credit_card

#### 添加一张信用卡

	POST /orgs/<org_id>/credit_cards

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|card_id|string |yes|||

返回结果：

	Status: 200 OK
	{
		"credit_id": "",
		"created" :""
	}

#### 查询信用卡列表

	GET /orgs/<org_id>/credit_cards


返回结果：

	Status: 200 OK
	{
		"cards": [
			{
				"card_id": "",
				"created": "",
				"updated": "",
			},
		...
		],
		"page": ,
		"per_page": ,
		"total": ,
	}

#### 获取信用卡详细信息

	GET /orgs/<org_id>/credit_cards/<credit_id>


返回结果：

	Status: 200 OK
	{
		"credit_card":
		{
			"card_id": "",
			"created": "",
			"updated": "",
			"account_info":[
				{
					"card_account_id": '',
					"credit_id": ''
					"media": '',
					"account_id": ''
				},
				...
			]
		},
		...
	}


#### 获取没有代理 agency 的 AdAccount 列表

        GET /orgs/<org_id>/credit_card_settlements/account_selection

返回结果：

    Status: 200 OK
	[
		'1',
		'2',
		...
	]

### credit_card_account

#### 查询信用卡绑定账户列表

	GET /orgs/<org_id>/credit_cards/<credit_id>/ad_accounts

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer |no|1|页号|
|per_page|integer |no|10|每页条数|
|filter_by|string |no||筛选|
|order_by|string |no||排序规则|

返回结果：

	Status: 200 OK
	{
		"card_accounts": [
			{
				"card_account_id": "",
				"credit_id": ""，
				"media": "",
				"account_id": "",
				"created": "",
				"updated": "",
			},
		...
		],
		"page": ,
		"per_page": ,
		"total": ,
	}

#### 信用卡绑定账户列表

	POST /orgs/<org_id>/credit_cards/<credit_id>/ad_accounts

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
| media_and_accounts| list(dict)|---|---| [{'media': '','account_id': ''}, {}]|

返回结果：


#### 修改信用卡绑定账户

	PUT /orgs/<org_id>/credit_cards/<credit_id>/accounts/<card_account_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|media|string |yes||投放平台|
|account_id|string |yes||投放账户 ID|

返回结果：

	Status: 200 OK

#### 删除信用卡绑定账户

	DELETE /orgs/<org_id>/credit_cards/<credit_id>/accounts/<card_account_id>

返回结果：

	Status: 200 OK


### credit_card_settlement

#### 查询结算记录列表

	GET /orgs/<org_id>/credit_card_settlements

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer |no|1|页号|
|per_page|integer |no|10|每页条数|
|filter_by|string |no||筛选|
|order_by|string |no||排序规则|

返回结果：

	Status: 200 OK
		{
		"settlements": [
			{
				"credit_id": ""
				"card_id": "",
				"settle_month": "",
				"total": "",
				"created": "",
				"updated": "",
			},
		...
		],
		"page": ,
		"per_page": ,
		"total": ,
	}

#### 查询结算记录详情

	GET /orgs/<org_id>/credit_card_settlements/<settle_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|order_by|string |no||排序规则|
|save_csv|string |no||True or False|


返回结果：

	Status: 200 OK
	{
		'card_billings':[
			{
				'manager_id'
				'account_i'
				'media'
				'country'
				'create_date'
				'spend'
				'updated'
				'created'
			}
		...
		]
		'total':
	}

	Status: 200 OK
	Response Stream



API


 代理与合同管理

#### 添加新的合同

        POST /orgs/<org_id>/agency_contracts

请求参数：

| Name         | Type                | Required | Default Value | Description  |
| ------------ | -----------         | -------- | ------------- | ------------ |
| contract_name| string              | yes      |               |合同中规定的代理名字      |
| compamy_id| int              | yes      |               ||
| rebate_type  | integer             | yes      |               |返点结算类型 1 是 Facebook， 2 是 Dvip 3 是 psp|
| items        | list(dict) ItemInfo | yes      |               |合同内容       |

##### ItemInfo

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|season| list string|yes||格式 ['201801-201803', '201804-201806']|
|coefficient|json format: {"5000_": "0.60", "0_3000": "0.55", "3000_5000": "0.60"}|no||FB 与 PSP 的系数|
|region|json format: {"country": "percent"}|no|| P-Vip 的 系数|

返回结果：

    Status: 200 OK


#### 获取所有合同列表

        GET /orgs/<org_id>/agency_contracts

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| page      | integer | no       | 1             | 页号        |
| per_page  | integer | no       | 10            | 每页条数     |
| order_by  | string  | no       | 无            | 排序规则     |
| filter_by | string  | no       | 无            | 筛选        |


返回结果：

    Status: 200 OK
    {
    	'agency_contracts': [
    		{
			 'contract_id': '',
    		 'contract_name':'',
    		 'rebate_type':'',
       		 'items':[
       		 		{
       		 			'season': '',
       		 			'coefficient': '',
       		 		}
       		 		...
       		 	],
       		 },
       		...
       ],
       'page': '',
       'per_page': '',
       'total': ''
    }

#### 获取单个合同信息

        GET /orgs/<org_id>/agency_contracts/<contract_id>


返回结果：

    Status: 200 OK
	{
		 'contract_id':'',
		 'contract_name':'',
		 'rebate_type':'',
		 'items':[
		 		{
		 			'season': '',
		 			'coefficient': '',
		 		}
		 		...
		 	],
	 },

#### 修改单个合同信息

        PUT /orgs/<org_id>/agency_contracts/<contract_id>

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| items     | list(dict) ItemInfo | yes      |               |合同内容       |


##### ItemInfo

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|season| string|yes||季度|
|coefficient|json format: {"5000_": "0.60", "0_3000": "0.55", "3000_5000": "0.60"}|no||FB 与 PSP 的系数|
|region|json format: {"country": "percent"}|no|| P-Vip 的 系数|

返回结果：

    Status: 200 OK
	{
		'contract_id': '',
		'updated': ''
	 },


返点流程

#### submit 提交 RebateSettlement

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/submitted

返回结果：

    Status: 200 OK

#### 上传 invoice 发票

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/invoice

请求参数：

| Name         | Type        | Required | Default Value | Description  |
| ------------ | ----------- | -------- | ------------- | ------------ |
|invoice       |json         | yes      |formart: {"invoice": file, "file_name": ""}|发票|

返回结果：
```
    Status: 200 OK
{
    "file_name": "rebate_invoice",
    "file_type": "image/png",
    "url": "http://localhost/v1/orgs/44/rebate_settlements/1/invoice/f0a0687c503a4b4e9c5ca7db71b89dd2.png"
}
```

#### 下载 invoice 发票

        GET /orgs/<org_id>/rebate_settlements/<settle_season_id>/invoice/<file_id>

请求参数：

| Name         | Type        | Required | Default Value | Description  |
| ------------ | ----------- | -------- | ------------- | ------------ |
|file_id       |string         | yes      |                 |发票|

返回结果：

    Status: 200 OK

#### review 评审 RebateSettlement

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/reviewed

返回结果：

    Status: 200 OK

#### pass 通过 RebateSettlement

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/passed

返回结果：

    Status: 200 OK

#### reject 拒绝 RebateSettlement

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/rejected

返回结果：

    Status: 200 OK


返点计算过程

#### 新建某季度返点结算

        POST /orgs/<org_id>/rebate_settlements

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| settle_season    | string | yes  |               | 季度      |
| contract_id| integer | yes  |               | 合同 ID      |

返回结果：

    Status: 200 OK

#### 获得某季度返点结算的列表

        GET /orgs/<org_id>/rebate_settlements

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| page      | integer | no       | 1             | 页号          |
| per_page  | integer | no       | 10            | 每页条数        |
| order_by  | string  | no       | 无             | 排序规则        |
| filter_by | string  | no       | 无             | 筛选          |

返回结果：

    Status: 200 OK
    {
    	'rebate_settlements': [
    		{
    		 'settle_season_id':'',
    		 'settle_season':'',
    		 'contract_id':'',
    		 'contract_name':'',
    		 'status': '',
    		 'amount':'',
    		 'created':'',
    		 'updated':'',
       		 },
       		...
       ],
       'page': '',
       'per_page': '',
       'total': ''
    }


#### 获得单个返点结算的详细信息

        GET /orgs/<org_id>/rebate_settlements/<settle_season_id>

返回结果：

    Status: 200 OK
	{
		 'settle_season_id':'',
		 'settle_season':'',
		 'contract_id':'',
		 'contract_name':'',
		 'status': '',
		 'amount':'',
		 'created':'',
		 'updated':'',
    },

#### 获得单个返点结算的对应的所有 account 条目信息

        GET /orgs/<org_id>/rebate_settlements/<settle_season_id>/ad_accounts

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| page      | integer | no       | 1             | 页号          |
| per_page  | integer | no       | 10            | 每页条数        |
| order_by  | string  | no       | 无             | 排序规则        |
| filter_by | string  | no       | 无             | 筛选          |

返回结果：

    Status: 200 OK
	{
    	'ad_accounts': [
    		{
    		 'settle_season_id':'',
    		 'account_id':'',
    		 'account_status':'',
    		 'contract_id':'',
    		 'contract_name': '',
    		 'item':'',
    		 'settle_info':'',
    		 'total':'',
    		 'amount':'',
    		 'created':'',
    		 'updated':'',
       		 },
       		...
       ],
       'page': '',
       'per_page': '',
       'total': ''
    },

#### 获得单个返点结算的对应的某个 account 条目信息

        GET /orgs/<org_id>/rebate_settlements/<settle_season_id>/ad_accounts/<account_id>

返回结果：

    Status: 200 OK
	{
		 'settle_season_id':'',
		 'account_id':'',
		 'account_status':'',
		 'contract_id':'',
		 'contract_name': '',
		 'item':'',
		 'settle_info':'',
		 'total':'',
		 'amount':'',
		 'created':'',
		 'updated':'',
		 },


#### 获得单个返点结算的对应的某个 account 条目下某个国家的信息

        GET /orgs/<org_id>/rebate_settlements/<settle_season_id>/ad_accounts/<account_country_id>


返回结果：

    Status: 200 OK
	{
		'account_country_id':'',
		'settle_season':'',
		'account_id':'',
		'country':'',
		'total':'',
		'first_change':'',
		'coefficient':'',
		'second_change':'',
		'values':'',
		'created':'',
		'updated':'',
    },

#### 上传 csv

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/csv

请求参数：

| Name         | Type        | Required | Default Value | Description  |
| ------------ | ----------- | -------- | ------------- | ------------ |
|csv       | file        | yes      |    | csv 核减信息|

返回结果：

    Status: 200 OK


#### 返点计算前期流程 -- 返点计算准备

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/ad_accounts/<account_id>/pre_settlement

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| pre_settle_info| PreSettleInfo | yes  |               | 流程数据      |

**此表作为下面所有的账户返点计算的参照**

RetbateType 为 facebook 时：

| PreSettleInfo      | type       | description |
| -------------   | ---------  | ----------- |
| increases       | json array | 核增项       |
| decreases       | json array | 核减项       |
| reduct_reset_revenue | integer   | 0 流水置为 0，1 取消变更 |
| reduct_reset_forfeit | integer   | 0 罚金置为 0，1 取消变更  |
| forfeit           | decimal   |                      |
| coupon               | decimail   | 优惠券额度    |


RebateType 为 adwords_dvip 时：

| PreSettleInfo      | type       | description |
| -------------   | ---------  | ----------- |
| increases       | json array | 核增项       |
| decreases       | json array | 核减项       |
| revenue_total   | decimal    | 封户判断后的流水      |
| reduct_reset_revenue | integer   | 0 流水置为 0，1 取消变更  |


RebateType 为 adwords_psp 时：

| PreSettleInfo       | type       | description |
| -------------   | ---------  | ----------- |
| increases       | json array | 核增项       |
| decreases       | json array | 核减项       |


返回结果：

    Status: 200 OK

#### 返点计算后期流程 -- 返点计算

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/ad_accounts/<account_id>/settlement

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| settle_info| SettleInfo | yes  |               | 流程数据      |


| SettleInfo       | type       | description |
| -------------   | ---------  | ----------- |
| increases       | json array | 提交前核增项       |
| decreases       | json array | 提交前核减项       |

返回结果：

    Status: 200 OK

#### 保存整个合同算出的返点值

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/compution

返回结果：

    Status: 200 OK

#### 退回到第一步流程全清第二三步的数据

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/previous

返回结果：

    Status: 200 OK

#### Dvip 时对单个国家的花费金额进行核增核减

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/ad_accounts/<account_id>/first_verify/<country_account_id>
 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| increases       | json array ||| 提交前核增项       |
| decreases       | json array ||| 提交前核减项       |

返回结果：

    Status: 200 OK


#### Dvip 时对单个国家的返点进行核增核减

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/ad_accounts/<account_id>/second_verify/<country_account_id>
 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| increases       | json array ||| 提交前核增项       |
| decreases       | json array ||| 提交前核减项       |

返回结果：

    Status: 200 OK
