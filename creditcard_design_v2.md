### API

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


