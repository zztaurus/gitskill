### API

#### 获取 AdAccount 列表

        GET /ad_accounts

返回结果：

    Status: 200 OK
    {
    	'ad_accounts': [
    	  {
    	    ...
          },
       ]
    }

    
#### 获取 Account 列表

        GET /orgs/<org_id>/ad_accounts

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
    		{	
				'media_account_id': '',
				'media_id': '',
				'account_id':'',
				'account_name',
				'payer': '',
				'payee': '',
				'default_payee': ''
				'media_name':'',
				'currency': '',
				'timezone': '',
				'account_type': '',
				'optimization_agency': '',
				'advertiser': '',
				'reseller': '',
				'contract_id': '',
				'contract_name': '',
				'card_id': '',
				'status': '',
				'disable_reason': '',
				'current_changed_date':'',
				'policy_risk_level': '',
				'product_num': '',
				'updated': "",
				'created': "",
         },
         ...
       ]
       'total': ''
       'page': ''
       'per_page': ''
    }

####  获取 AdAccount详情
        GET  /orgs/<org_id>/ad_accounts/<media_account_id>
	
返回结果:
	 
	Status: 200 OK
	{
		'media_account_id': '',
		'account_id': '',
		'account_name': '',
		'agency_type': '',
		'advertiser_id': '',
		'advertiser_name': '',	
		'credit_card_id': '',
		'card_id': '',
		'optimization_agency_info': [
			{
				'company_id': '',
				'company_name': '',
				'effective_date': '',
				'media_account_id': ''
			},			
		],
		'reseller_info': [
			{
				'company_id': '',
				'company_name': '',
				'effective_date': '',
				'contract_id': '',
				'contract_name': ''
			},
		]
		
				}

####  修改 AdAccount
        PUT  /orgs/<org_id>/ad_accounts/<media_account_id>

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
|account_type| interger | yes | no | 账户类型 | 
|account_name      | string |no       | no            |账户名称         |
|advertiser_id      | interger |yes       | no            |   广告主ID     |
|credit_card_id      | interger |no       | no            |    信用卡账户   |
|optimization_agency_info     | json array |no       | no            | |
|reseller_info | json arry | no | no |


返回结果：

    Status: 200 OK

#### 批量修改 AdAccount

        PUT /orgs/<org_id>/ad_accounts/batch_changed

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
|account_ids      | json array |yes       | no            |media_account_id 列表         |
|account_type| interger | yes | no | 账户类型 | 
|advertiser_id      | interger |yes       | no            |   广告主ID     |
|credit_card_id      | interger |no       | no            |    信用卡账户   |
|optimization_agency_info     | json array |no       | no            | |
|reseller_info | json arry | no | no |


返回结果：

    Status: 200 OK
    
    
### AdAccount Model Design

#### `Media`

| Field         | type      | Desc   | Unique  | Index     | Null    |
| ------------- | --------- | -------| ------- | --------- | ------- |
| media_id   | interger | 平台属性ID | yes    | yes   | no   |      |
| name | varchar(50) | 平台属性名称 | no | yes | no |
| updated      | datetime     | 更新时间 | no     | no   | no   |   
| created      | datetime     | 创建时间 | no     | yes   | no   |  

#### `AdAccount`

| Field         | type      | Desc   | Unique  | Index     | Null    |
| ------------- | --------- | -------| ------- | --------- | ------- |
| media_account_id | interger | 自增主键 | yes | yes | no |
| account_id   | varchar(100)   |    账号ID  | no      | yes       | no      |
| media_id   | interger | 所属平台属性ID | no    | yes   | no   |
| managers   | list dict   |  账号所属的manger_id list | no      | yes       | no      |
| account_name   | varchar(100)   |    账号名称   | no      | yes       | yes      |
| account_type   | varchar(100)   |    账号类型   | no      | yes       | yes      |
| agency_type   | varchar(12)   |  opua 或 outsource   | no      | yes       | no      |
| advertiser_id | interger | 广告主ID | no | yes | yes |
| timezone | varchar(50) | 账号当前时区 | no | yes | yes|
| currency | varchar(50) | 账号所使用的货币 | no | yes | yes|
| disable_reason | interger | 封户原因(有对照map) | no | yes | yes|
| status       | integer | 广告账户状态：1 为 正常 enable； 2 为 封户 disable 3 为未绑定 unbinding| no | yes    | no   |
| current_changed_date  | datetime     | 状态改变更新时间              | no     | yes   | no   |     
| status_changed_history  | list dict     | 状态改变 [{date, (status1, status2)}] | no     | yes   | no   |
| policy_risk_level  | varchar(50)     | 账户政策风险 | no     | yes   | yes   |  
| updated      | datetime     | 更新时间 | no     | no   | no   |   
| created      | datetime     | 创建时间 | no     | yes   | no   |

注：account_id media_id 联合唯一索引    

#### `AdAccountFinanceMap`

| Field         | type      | Desc   | Unique  | Index     | Null    |
| ------------- | --------- | -------| ------- | --------- | ------- |
| media_account_id | interger | 主键 | no | yes | no |
| account_id | varchar(100) | 账号ID | no | yes | no |
| media_id   | interger | 所属平台属性ID | no    | yes   | no   |
| payer_id | interger | 公司内部付款方 | no | yes | no |
| payee_id | interger | 付款方 | no | yes | no |
| credit_card_id | interger | 信用卡ID | no | yes | no |
| default_payee | interger | 收款方 | no | yes | yes |
| current_agency | interger | 最新的optimization agency的ID | no | yes | yes |
| current_reseller | interger | 最新的reseller的ID | no | yes | yes |
| current_contract | interger | 最新的contract的ID | no | yes | yes |
| updated      | datetime     | 更新时间 | no     | no   | no   |   
| created      | datetime     | 创建时间 | no     | yes   | no   | 

#### `AdAccountOptimizationAgencyMap`

| Field         | type      | Desc   | Unique  | Index     | Null    |
| ------------- | --------- | -------| ------- | --------- | ------- |
| media_account_id | interger | 主键 | no | yes | no |
| account_id | varchar(100) | 账号ID | no | yes | no |
| media_id   | interger | 所属平台属性ID | no    | yes   | no   |
| company_id | interger | 广告账户实际操作的company_id 主键 | no | yes | no |
| effective_date      | datetime     | 生效时间  主键| no     | yes   | no   |   
| expiration_date      | datetime     | 截止时间 | no     | yes   | yes   | 
| updated      | datetime     | 更新时间 | no     | no   | no   |   
| created      | datetime     | 创建时间 | no     | yes   | no   | 

#### `AdAccountResellerMap`

| Field         | type      | Desc   | Unique  | Index     | Null    |
| ------------- | --------- | -------| ------- | --------- | ------- |
| media_account_id | interger | 主键 | no | yes | no |
| account_id | varchar(100) | 账号ID | no | yes | no |
| media_id   | interger | 所属平台属性ID | no    | yes   | no   |
| company_id | interger | 非媒体广告账户开设者的company_id 主键| no | yes | no |
| contract_id | interger | 关联的合同ID | no | yes | no |
| effective_date      | datetime     | 生效时间 主键| no     | yes   | no   |   
| expiration_date      | datetime     | 截止时间 | no     | yes   | yes   | 
| updated      | datetime     | 更新时间 | no     | no   | no   |   
| created      | datetime     | 创建时间 | no     | yes   | no   | 

#### `BillingOfAdAccount`

| field        | type         | description                                                  | unique | index | NULL |
| ------------ | ------------ | ------------------------------------------------------------ | ------ | ----- | ---- |
| account_id   | varchar(100)  | 广告账户 id  主键                                                  | no    | yes   | No   |
| media       | varchar(10)   | 平台 主键                                                         | no     | yes   | no   |
| create_date         | datetime     | 日期   主键                                                      | no    | yes   | yes   |   
| spend        | decimal      | 按照日期抓取的流水                                                | no    | no   | no   |     
| updated      | datetime     | 更新时间                                                     | no     | no   | no   |      
| created      | datetime     | 创建时间                                                     | no     | yes   | no   |     









































