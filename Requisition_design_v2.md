## API
          
### 获取公司付款基本信息列表

    GET  /orgs/<org_id>/companies/<company_id>/payment_infos

#### 请求参数

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer|no|1|页号|
|per_page|integer|no|10|每页条数|
|order_by|string|no||排序规则|
|filter_by|string|no||筛选|
|columns|string|no||展示字段|

### 返回结果：

    Status: 200 OK 
    
    {
       "payment_infos":[
           {
             "payment_id":''
             "config_name"：'',
             "currency_type":'',
             "application_description":'',
             "payee":'',
             "due_bank":'',
             "bank_account":'',
             "swift_code":'',
             "bank_address":'',
             "inward_prompt":'',
             "external_prompt": '',
             "credit_term":'',
             "contract_status":'',
             "special_approver":''
           }
           ...
       ]
      "page": ,
      "per_page": ,
      "total": ,
    }
    
### 配置公司付款基本信息
    
    Post  /orgs/<org_id>/companies/<company_id>/payment_infos  
    
#### 请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
| config_name | string | yes |  | 基本付款信息配置类型 |
| currency_type | string | yes | | 货币类型|
| application_description | string | yes | | 申款用途|
| payee | string | yes | | 收款人 |
| due_bank | string | yes | | 收款银行 |
| bank_account | string | yes | | 收款银行账户|
| swift_code | string | yes | | 银行通信编码|
| bank_address | string | yes | | 银行地址|
| inward_prompt| string | yes | | 对内提示vendor公司名|
| external_prompt | string | yes | | 对外提示公司名|
| credit_term | int | yes | | 账期 |
| contract_status |int| yes | | 是否签订合同|
| special_approver |string | yes | | 超出方法论审批人|

#### 返回结果：
    
    Status：200 OK 
    

### 获取一条付款基本信息

    GET  /orgs/<org_id>/companies/<company_id>/payment_infos/<payment_id>

### 返回结果：

    Status: 200 OK 
    
    {
       "payment_info":
           {
             "config_name"：'',
             "currency_type":'',
             "application_description":'',
             "payee":'',
             "due_bank":'',
             "bank_account":'',
             "swift_code":'',
             "bank_address":'',
             "inward_prompt":'',
             "external_prompt": '',
             "credit_term":'',
             "contract_status":'',
             "special_approver":''
           }
    }
    
### 更新一条付款基本信息
    
    put  /orgs/<org_id>/companies/<company_id>/payment_infos<payment_id>
    
#### 请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
| currency_type | string | yes | | 货币类型|
| application_description | string | yes | | 申款用途|
| payee | string | yes | | 收款人 |
| due_bank | string | yes | | 收款银行 |
| bank_account | string | yes | | 收款银行账户|
| swift_code | string | yes | | 银行通信编码|
| bank_address | string | yes | | 银行地址|
| inward_prompt| string | yes | | 对内提示vendor公司名|
| external_prompt | string | yes | | 对外提示公司名|
| credit_term | int | yes | | 账期 |
| contract_status |int| yes | | 是否签订合同|
| special_approver |string | yes | | 超出方法论审批人|

#### 返回结果：
    
    Status：200 OK 
    
### 配置部门请款的发件人和抄送人信息

    PUT /payment_configs

#### 请求参数：

| Name | Type | Required | Default Value | Description | 
| ---- | ---- | -------- | ------------- | ----------- |
| org_id | int | yes | | 配置部门 | 
| mail_info | json dict  | yes | | 发送人和抄送人信息 |


#### 返回结果：

    Status: 200 OK 
    
    
### 获取请款单列表

    GET /orgs/<org_id>/requisitions
    
#### 请求参数

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer|no|1|页号|
|per_page|integer|no|10|每页条数|
|order_by|string|no||排序规则|
|filter_by|string|no||筛选|
|columns|string|no||展示字段|
    
#### 返回结果：

    Status：200 OK
    {
      
      ‘requisitions’:[
          {
              "requisition_id":'',
              "application_department":'',
              "month":''
              "pay_to":'',
              "media":'',
              "amount_spent":'',
              "rebate_amount":'',
              "amounts_payable":'',
              "notes":'',
              "status":'',
              "updated":'',
              "created":''
          }
          ...
      ]
      "page": ,
      "per_page": ,
      "total": ,
    }
    
### 获取请款单详情

     GET /orgs/<org_id>/requisitions/<requisition_id>
     
#### 返回结果：

    Status：200 OK
    {
        "requisition":{
          "requisition_id":'',
          "application_department":{},
          "month":''
          "pay_to":{},
          "config_name":'',
          "media":'',
          "amount_spent":'',
          "rebate_amount":'',
          "amounts_payable":'',
          "notes":'',
          "attach_files": ['','',...],
          "credit_term": '',
          "contract_status":'',
          "invoice_status":'',
          "status":'',
          "subject":'',
          "to":'',
          "cc":'',
          "applicant":{}
          "payment_setting":[{},....]
          "status_info":[{},.....]
          "updated":'',
          "created":''  
        }    
    }
    

    
### 新建请款单

    POST /orgs/<org_id>/requisitions
    
#### 请求参数

| Name | Type | Required | Default Value | Description | 
| ---- | ---- | -------- | ------------- | ----------- |
| application_department | int |yes | | 当前请款部门 |
| month |string | yes | | 请款单月份|
| pay_to | int | yes | | 付款对象(公司) |
| config_name | string | yes | | 基本付款信息配置类型 |
| media | string | yes | | 媒体 |
| amount_spent | decimal | yes | | 账户话费金额 | 
| rebate_amount | decimal | yes | | 返点抵扣金额 |
| amounts_payable | decimal | yes | | 实际应付金额 | 
| notes | json dict {'text':''} | | | 说明|
| attach_files | list string | | | 上传文件列表 |
| credit_term |int | yes | | 账期 | 
| contract_status | integer | yes | | 是否签订合同 |
| invoice_status | integer | yes | | 通知状态 |
| subject | string | yes | | 请款单主题 |

#### 返回结果:

    Status: 200 OK 
    
    {
        "requisition_id":'',
        "created":""
    }
    
    
### 更新请款单

    PUT /orgs/<org_id>/requisitions/<requisitions_id>
    
####  请求参数：

| Name | Type | Required | Default Value | Description | 
| ---- | ---- | -------- | ------------- | ----------- |
| media | string | yes | | 媒体 |
| amount_spent | decimal | yes | | 账户花费金额 | 
| rebate_amount | decimal | yes | | 返点抵扣金额 |
| amounts_payable | decimal | yes | | 实际应付金额 | 
| notes | json dict  | | | 说明|
| attach_files | list string | | | 上传文件列表 |
| credit_term | int | yes | | 账期 | 
| contract_status | integer | yes | | 是否签订合同 |
| invoice_status | integer | yes | | 通知状态 |

    
#### 返回结果:

    Status: 200 OK 
    
### 提交请款单 

    PUT /orgs/<org_id>/requisitions/<requisition_id>/submit
    
#### 返回结果：

    Status: 200 OK 
  
### 拒绝请款单 

    PUT /orgs/<org_id>/requisitions/<requisition_id>/reject

### 请求参数

| Name | Type | Required | Default Value | Description | 
| ---- | ---- | -------- | ------------- | ----------- |
| comments | string | yes | | 批注 |
    
    
####返回结果：

    Status: 200 OK 

### Business VP review 请款单 

    PUT /orgs/<org_id>/requisitions/<requisition_id>/review

### 请求参数

| Name | Type | Required | Default Value | Description | 
| ---- | ---- | -------- | ------------- | ----------- |
| comments | string | yes | | 批注 |
    
#### 返回结果：

    Status: 200 OK 
    
### Finance Leader review 请款单 

    PUT /orgs/<org_id>/requisitions/<requisition_id>/passed

### 请求参数

| Name | Type | Required | Default Value | Description | 
| ---- | ---- | -------- | ------------- | ----------- |
| comments | string | yes | | 批注 |
    
    
#### 返回结果：

    Status: 200 OK 
    
    
### 请款单上传附件


    POST /orgs/<org_id>/requisitions/files
    
####请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|file|File|yes||文件流|

####返回结果：

    Status: 200 OK
    {
      "file_name": "",
      "url": "http://xxxx"
    }


### 请款单附件下载

    GET /orgs/<org_id>/requisitions/files/<file_id>

#### 返回结果：
    
    Status: 200 OK  
    
## Model

### PaymentSetting

| field | type | description | unique | index | NULL |
| ----- | ---- | ----------- | ------ | ----- | -----|
| payment_id | integer | 主键 | yes | yes | no |
| company_id | integer | 公司 id | no | yes | no |
| config_name | varchar(30) | 付款信息配置名称 (eg：all 表示所有media)| yes | yes | no |
| currency_type | varchar(10) | 货币类型 | no | yes | no |
| application_description | varchar(100) | 申款用途 | no | no | no |
| payee | varchar(100) | 收款人 | no | yes | no |
| due_bank | varchar(100) | 收款银行 | no | no | no |
| bank_account | varchar(100) | 收款银行账户 | no | no | no |
| swift_code | varchar(100) | 银行通信编码 | no | no | no |
| bank_address | varchar(100) | 银行地址 | no | no | no |
| internal_prompt | varchar(50) | 对内提示vendor公司名 | no | no | no |
| external_prompt | varchar(50) | 对外提示公司名 | no | no | no |
| credit_term | integer | 账期 天数 | no | no | no |
| contract_status | integer | 是否签订合同 (1:yes 0:no)| no | no | no |
| special_approver | srting | 超出方法论审批人 | no | no | no | 

#### Requisition

| field | type | description | unique | index | NULL |
| ----- | ---- | ----------- | ------ | ----- | ---- |
| requisition_id | integer | 请款单 id  主键 | yes | yes | no |  
| application_department| integer | 请款部门id| no | yes | no | 
| month | datetime | 请款单月份 | no | yes | no| 
| pay_to | integer | 付款对象 (公司)| no | yes | no |
| config_name |varchar(30) |付款基本信息配置 | yes | no | no |
| media | varchar(20) |  媒体 | no | yes | no |
| amount_spent |double | 账户花费金额 | no | no | no | 
| rebate_amount | double | 返点抵扣金额 | no | no | no |
| amounts_payable | double | 实际应付金额 | no | no | no |
| notes | json dict | 说明（发送邮件时作为邮件正文） | no | no | |
| attach_files | json list | 上传文件url和file_name的列表 | no | no |  |
| credit_term | datetime | 账期 只可选择：Expedited（30 days）/Normal（45 days）/ delayed（60 days）| no | no | no |
| contract_status | integer | 是否签订合同 (1为签订 2为未签订)| no | yes | no |
| invoice_status | integer | 通知状态(1:yes 2:no) | no | yes | no |
| status | integer | 请款单流程状态 | no | yes | no |
| subject | varchar(100) | 请款主题 | yes | yes | no |
| to | json | 发件人列表 | no | no | no | 
| cc | json | 抄送人列表 | no | no | no |
| applicant | integer | 请款人 user_id | no | yes | no |
| payment_setting | json | 基本付款信息 | no | no | no |
| status_info | json | 请款单操作记录 | no | no | |
| updated | datetime | 更新时间 | no | yes | no |
| created | datetime | 创建时间 | no | yes | no | 



