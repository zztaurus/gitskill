### API

### 合同内容

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


### 返点流程


#### 新建某季度返点结算

    POST /orgs/<org_id>/rebate_settlements

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| settle_season    | string | yes  |               | 季度      |
| contract_id| integer | yes  |               | 合同 ID      |

返回结果：

    Status: 200 OK
    {
    	RebateSettlementInfo
    }

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
    

#### 修改单个返点结算信息
	
	PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>
	
请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| notes    | json dict | yes  |               |   {"text": "", "pictures": []}    |


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

#### 返点计算前期流程 -- 返点计算准备

        PUT /orgs/<org_id>/rebate_settlements/<settle_season_id>/ad_accounts/<account_id>/pre_settlement

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| pre_settle_info| PreSettleInfo | yes  |               | 流程数据      |
| median| decimal  | no  |      | 计算过程中的中间值      |

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
    
    
### Model 

#### Contract

| field        | type         | description | unique | index | NULL | 
| ------------ | ------------ | -------| ------ | ----- | ---- | ---- |
| contract_id  | interger    |  合同编号，主键 | yes      | yes       | no      |
| contract_name | varchar(50) |  合同名字  | yes | yes | no    |
| rebate_type | integer |1 为 facebook，2 为 adwords_dvip, 3 为 adwords_psp| no | yes        | no     |
| company_id  | interger    |  代理公司ID | yes      | yes       | no      |
| org_id  | interger    |  所属组织ID | yes      | yes       | no      |
| org_name | varchar(100) |  组织名字  | yes | yes | no    |
| company_name | varchar(100) |  公司别名  | yes | yes | no    |
| legel_name | varchar(100) |  公司名字  | yes | yes | no    |
| items| json array| item 列表  | no      | no        | yes     |
| created       | datetime  | 创建时间  | no      | yes       | no      |
| updated       | datetime  | 更新时间  | no      | no        | no      |

#### SettlementOfRebate


| Field         | type      | description | unique  | index     | Null    |
| ------------- | --------- | ------------| ------- | --------- | ------- |
| settle_season_id  | interger | 返点结算 id, 主键 | no   | yes       | no      |
| settle_season   | varchar(50)    | 返点结算季度 | no      | yes       | no      |
| org_id  | interger    |  所属组织ID | yes      | yes       | no      |
| org_name | varchar(100) |  组织名字  | yes | yes | no    |
| contract_id        | interger    |  | no      | yes       | no      |
| contract_name      | varchar(50) |  | no      | yes       | no      |
| items| json array| item 列表  | no      | no        | yes     |
| status       | integer   | 返点结算状态 | no      | yes        | no     |
| amount     | decimal| 金额 | no      | no        | yes     |
| total_billing | decimal | 页面修正总金额 | no | no | yes | 
| coefficient     | decimal| 返点系数 | no      | no        | yes     |
| notes| json array| 上传的附件和文本信息  | no      | no        | yes     |
| extra| json array| 其他  | no      | no        | yes     |
| status_info | json array | 审批记录 | no | no | yes |
| created       | datetime  | 创建时间 | no      | yes       | no      |
| updated       | datetime  | 更新时间  | no      | no        | no      |

#### SettlementOfRebateAdAccount

| Field         | type      | description | unique  | index     | Null    |
| ------------- | --------- | ------------| ------- | --------- | ------- |
| settle_season_id | interger    | 返点结算 id，主键 | no      | yes       | no      |
| account_id | varchar(50)    | 广告账户， 主键  | no      | yes       | no      |
| media | varchar(50)    | 所属平台  | no      | yes       | no      |
| account_status | integer   | 广告账户状态| no      | yes       | no      |
| contract_id | interger    |  合同ID | no      | yes       | no      |
| contract_name | varchar(50)    |  合同名称 | no      | yes       | no      |
| pre_settle_info  | PreSettleInfo  | 预返点信息 | no      | yes        | no     |
| median | decimal | total 经过 Pre 计算后中间值 | no      | yes        | no     |
| settle_info | SettleInfo| 返点信息 | no      | yes        | no     |
| amount | decimal | 最终返点额度 | no      | yes        | no     |
| time_scale| json array| 时间区间  | no      | no        | yes     |
| paymeng_info| json array|  | no      | no        | yes     |
| summary | decimal |  | no      | yes        | no     |
| created | datetime | 创建时间 | no      | yes       | no      |
| updated | datetime  | 更新时间 | no      | no        | no      |





















