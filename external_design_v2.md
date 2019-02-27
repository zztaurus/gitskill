### API

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

