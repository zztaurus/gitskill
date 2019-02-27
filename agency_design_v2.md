### API

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
	
	
### Model

### `SettlementOfAgency`

| Field | Type | Description | Unique | Index | Null |
| ------| -----| ------------| -------| ------| -----|
| settle_id | integer| 主键 | yes | yes | no |
| settle_month | varchar(10) |  对代理付款月份 | no | yes | no |
| org_id | integer | 部门 ID | no | yes | no |
| org_name | integer | 部门 名称 | no | yes | no |
| media  | varchar(50)| 投放平台 | no | yes | yes |
| company_id | integer | 代理公司 ID | no | yes | no |
| company_name | varchar(50)|  代理公司名称 | no | yes | no |
| status| integer| 付款流程的状态 | no | yes | no |
| summary | decimal| 对外付款总金额 | no | no | yes |
| amount | decimal | 对外付款最终总金额 | no | no | yes |
| notes | json dict | 说明 | no | no | yes|
| extra | json dict | 其他字段 | no | no | yes|
| status_info | json array | 审批记录 | no | no | yes | 
| company_category | interger | 代理公司类别 | no | yes | no |
| created| datetime| 创建时间 | no | yes | no |
| updated| datetime| 更新时间 | no | no| no |

联合唯一索引：org_id, settle_month, media, company_id
