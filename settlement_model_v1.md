### 账户管理设计方案

#### AdAccount
| field        | type         | description                                                  | unique | index | NULL |      |
| ------------ | ------------ | ------------------------------------------------------------ | ------ | ----- | ---- | ---- |
| account_id   | varchar(100)  | 广告账户 id                           | no    | yes   | No   |      |
| manager_id   | varchar(100) | manager 编号                          | no    | yes   | no   |      |
| media        | varchar(32)       | media                           | no     | yes   | no   |
| status       | integer | 广告账户状态：1 为 正常 enable； 2 为 封户 disable 3 为未绑定 unbinding| no | yes    | no   |      |
| current_changed_date  | datetime     | 状态改变更新时间              | no     | yes   | no   |      |
| all_changed_date  | list dict     | 状态改变 [{date, (status1, status2)}] | no     | yes   | no   |      |
| updated      | datetime     | 更新时间                             | no     | no   | no   |      |
| created      | datetime     | 创建时间                             | no     | yes   | no   |      |
主键：account_id, manager_id

#### AdAccountAgencyMap
| field        | type         | description                             | unique | index | NULL |      |
| ------------ | ------------ | --------------------------------------- | ------ | ----- | ---- | ---- |
| account_id   | varchar(100)  | 广告账户 id                             | no    | yes   | No   |      |
| manager_id   | varchar(100) | manager 编号                            | no    | yes   | no   |      |
| company_id   | interger   |    公司 ID                               | no      | yes       | no      |
| company_name | varchar(50)|   公司名称                                | no      | yes       | no      |
| effective_date | datetime     | 生效日期                               | no     | no   | no   |      |
| expiration_date | datetime     | 截止日期                               | no     | no   | no   |      |
| updated      | datetime     | 更新时间                               | no     | no   | no   |      |
| created      | datetime     | 创建时间                               | no     | yes   | no   |      |
主键：account_id, manager_id, company_id

#### AdAccountContractMap
| field        | type         | description                                                  | unique | index | NULL |      |
| ------------ | ------------ | ------------------------------------ | ------ | ----- | ---- | ---- |
| account_id   | varchar(100)  | 广告账户 id                          | no    | yes   | No   |      |
| manager_id   | varchar(100) | manager 编号                         | no    | yes   | no   |      |
| contract_id        | interger    |                               | no      | yes       | no      |
| contract_name| varchar(50)      |     合同规定的返点名字            | no    | yes   | yes   |      |
| effective_date | datetime     | 生效日期                          | no     | no   | no   |      |
| expiration_date | datetime     | 截止日期                         | no     | no   | no   |      |
| updated      | datetime     | 更新时间                            | no     | no   | no   |      |
| created      | datetime     | 创建时间                            | no     | yes   | no   |      |
主键：account_id, manager_id, contract_id

#### AccountBilling
| field        | type         | description                                                  | unique | index | NULL |      |
| ------------ | ------------ | ------------------------------------------------------------ | ------ | ----- | ---- | ---- |
| manager_id   | varchar(100) | manager 编号                                                  | no    | yes   | no   |      |
| account_id   | varchar(100)  | 广告账户 id                                                    | no    | yes   | No   |      |
| country       | varchar(10)   | 国家                                                           | no     | yes   | no   |      |
| create_date         | datetime     | 日期                                                          | no    | yes   | yes   |      |
| spend        | decimal      | 按照日期抓取的流水                                                | no    | no   | no   |      |
| updated      | datetime     | 更新时间                                                     | no     | no   | no   |      |
| created      | datetime     | 创建时间                                                     | no     | yes   | no   |      |
主键：manager_id, account_id, region, date

## 对外付款表结构设计

## Settlement

### `AgencySettlement`

| Field         | type      | description                                         | unique  | index     | Null    |
| ------------- | --------- | ----------------------------------------------------| ------- | --------- | ------- |
| settle_id     | integer   | 主键                                                 | yes      | yes       | no      |
| settle_month  | varchar(10)    |  对代理付款月份                                                   | no      | yes       | no      |
| org_id     | integer   |          自己的 ID                                        | yes      | yes       | no      |
| media         | varchar(50)    | 投放平台                                             | no      | yes       | yes     |
| company_id    | integer    |  代理公司 ID                                                   | no      | yes       | no      |
| company_name  | varchar(50)    |  代理公司名称                                                   | no      | yes       | no      |
| status        | integer   | 付款流程的状态                                        | no      | yes       | no      |
| total         | decimal   | 对外付款总金额                                        | no      | no        | yes     |
| amount         | decimal   | 对外付款最终总金额                                        | no      | no        | yes     |
| notes         | json dict | 说明                                                 | no      | no        | no     |
| created       | datetime  | 创建时间                                             | no      | yes       | no      |
| updated       | datetime  | 更新时间                                             | no      | no        | no      |

联合唯一索引：settle_month, media, company_id

### `ExternalSettlement`

| Field             | type      | description                                         | unique  | index     | Null    |
| ----------------- | --------- | ----------------------------------------------------| ------- | --------- | ------- |
| settle_id         | integer   | 主键                                                 | yes     | yes      | no      |
| settle_month      | varchar(10)    |   对外 advertims 付款的月份                                                  | no      | yes       | no      |
| org_id     | integer   |          自己的 ID                                        | yes      | yes       | no      |
| consumer_org_id  | integer    |  代理方 ID                                                   | no      | yes       | no      |
| company_id        | integer    |   外部公司 ID                                                  | no      | yes       | no      |
| company_name      | varchar(50)    |  外部公司名称                                                  | no      | yes       | no      |
| status            | integer   | 付款流程的状态                                        | no      | yes       | no      |
| total             | decimal   | 对外付款总金额                                        | no      | no        | yes     |
| notes             | json dict | 说明                                                 | no      | no        | no     |
| created           | datetime  | 创建时间                                             | no      | yes       | no      |
| updated           | datetime  | 更新时间                                             | no      | no        | no      |

联合唯一索引：settle_month, company_id, org_id

### `UAVendorSettlement`

| Field             | type      | description                                         | unique  | index     | Null    |
| ----------------- | --------- | ----------------------------------------------------| ------- | --------- | ------- |
| settle_id         | integer   | 主键                                                 | yes     | yes      | no      |
| settle_month      | varchar(10)    |  对外付款月份                                                   | no      | yes       | no      |
| org_id     | integer   |          自己的 ID                                        | yes      | yes       | no      |
| consumer_org_id  | integer    |  代理方 ID                                                   | no      | yes       | no      |
| company_id        | integer    |  外部投放公司 ID                                                  | no      | yes       | no      |
| company_name      | varchar(50)    |  外部公司名称                                                   | no      | yes       | no      |
| status            | integer   | 付款流程的状态                                        | no      | yes       | no      |
| total             | decimal   | 对外付款总金额                                        | no      | no        | yes     |
| notes             | json dict | 说明                                                 | no      | no        | no     |
| created           | datetime  | 创建时间                                             | no      | yes       | no      |
| updated           | datetime  | 更新时间                                             | no      | no        | no      |

联合唯一索引：settle_month, company_id

### `AgencyAccountSettlement`

| Field         | type      | description                                         | unique  | index     | Null    |
| ------------- | --------- | ----------------------------------------------------| ------- | --------- | ------- |
| settle_id         | interger    |   主键                                                  | no      | yes       | no      |
| settle_month         | varchar(10)    |  结算月份                                                  | no      | yes       | no      |
| account_id    | varchar(50)    |  账户 ID                                                  | no      | yes       | no      |
| account_status    | integer    | 广告账户状态：1 为 正常 enable； 2 为 封户 disable 3 为未绑定 unbinding| no    | no    | no   |      |
| total         | decimal   |   核减后对代理付款总金额                                                  | no      | no        | yes     |
| summary         | decimal   | 核减前对代理付款总金额                                                    | no      | no        | yes     |
| increases     | json array| 增项列表                                             | no      | no        | yes     |
| decreases     | json array| 减项列表                                             | no      | no        | yes     |
| created       | datetime  | 创建时间                                             | no      | yes       | no      |
| updated       | datetime  | 更新时间                                             | no      | no        | no      |

联合唯一索引：settle_month, account_id


### `CreditCard`
| Field         | type      | description                                         | unique  | index     | Null    |
| ------------- | --------- | ----------------------------------------------------| ------- | --------- | ------- |
| credit_id       | interger    |  主键                                 | yes      | yes       | no      |
| card_id       | varchar(50)    | 信用卡账户                                 | yes      | yes       | no      |
| created       | datetime  | 创建时间                                             | no      | yes       | no      |
| updated       | datetime  | 更新时间                                             | no      | no        | no      |

### `CreditCardAccount`

| Field         | type      | description                                         | unique  | index     | Null    |
| ------------- | --------- | ----------------------------------------------------| ------- | --------- | ------- |
| card_account_id       | interger    | 主键                                 | yes      | yes       | no      |
| credit_id       | varchar(50)    | 信用卡账户 ID                                           | no      | yes       | no      |
| media         | varchar(50)    | 投放平台                                             | no      | yes       | no      |
| account_id    | varchar(50)    | 投放账户 ID                                           | no      | yes       | no     |
| created       | datetime  | 创建时间                                             | no      | yes       | no      |
| updated       | datetime  | 更新时间                                             | no      | no        | no      |

### `CreditCardSettlement`

| Field         | type      | description                                         | unique  | index     | Null    |
| ------------- | --------- | ----------------------------------------------------| ------- | --------- | ------- |
| settle_id         | interger    |   主键                                                  | no      | yes       | no      |
| settle_month         | varchar(10)    |  结算月份                                                  | no      | yes       | no      |
| credit_id       | interger    | 信用卡账户 ID                                           | no      | yes       | no      |
| total         | decimal   |    信用卡付款总金额                                               | no      | no        | yes     |
| created       | datetime  | 创建时间                                             | no      | yes       | no      |
| updated       | datetime  | 更新时间                                             | no      | no        | no      |

联合唯一索引：settle_month, credit_id




## 返点计算

合同
### `AgencyContract`


| Field         | type      | description                                | unique  | index     | Null    |
| ------------- | --------- | -------------------------------------------| ------- | --------- | ------- |
| contract_id        | interger    |  合同编号，主键                    | yes      | yes       | no      |
| contract_name      | varchar(50) |  合同名字                                 | yes      | yes       | no      |
| rebate_type       | integer |1 为 facebook，2 为 adwords_dvip, 3 为 adwords_psp| no      | yes        | no     |
| items     | json array| item 列表                                        | no      | no        | yes     |
| created       | datetime  | 创建时间                                     | no      | yes       | no      |
| updated       | datetime  | 更新时间                                     | no      | no        | no      |


返点结算账单（每个合同对应的单个代理的合集）
### `RebateSettlement`


| Field         | type      | description                                | unique  | index     | Null    |
| ------------- | --------- | -------------------------------------------| ------- | --------- | ------- |
| settle_season_id    | interger    |         返点结算 id, 主键            | no      | yes       | no      |
| settle_season   | varchar(50)    |           返点结算季度                | no      | yes       | no      |
| contract_id        | interger    |                                      | no      | yes       | no      |
| contract_name      | varchar(50)    |                                   | no      | yes       | no      |
| status       | integer   |                    返点结算状态               | no      | yes        | no     |
| amount     | decimal| 金额                                             | no      | no        | yes     |
| total_billing | decimal | 返点依赖的总额度                               | no      | no        |  yes    | 
| created       | datetime  | 创建时间                                     | no      | yes       | no      |
| updated       | datetime  | 更新时间                                     | no      | no        | no      |

### `CountryAccountSettlement`

| Field         | type      | description                                         | unique  | index     | Null    |
| ------------- | --------- | ----------------------------------------------------| ------- | --------- | ------- |
| account_country_id| interger    |   主键                                        | no      | yes       | no      |
| settle_season_id    | interger    |         返点结算 id             | no      | yes       | no      |
| settle_season | varchar(10)    |  结算季度
| account_id    | varchar(50)    |  账户 ID                                       | no      | yes       | no      |
| country       | varchar(10)    |  国家                                    | no      | yes       | no      |
| total         | decimal        |    按国家付款总金额                             | no      | no        | yes     |
| amount         | decimal        |		核减之后的总金额                             | no      | no        | yes     |
| first_change  | json   |  核增核减                                          | no      | no       | yes      |
| coefficient   | decimal   |    按国家付款返点阶梯系数                           | no      | no        | yes     |
| second_change | json   |   核增核减                                            | no      | no       | yes      |
| value         | json ValueInfo |    金额计算的集合                                 | no      | no        | yes     |
| created       | datetime  | 创建时间                                             | no      | yes       | no      |
| updated       | datetime  | 更新时间                                             | no      | no        | no      |

联合唯一索引：settle_season_id, account_id, country

| ValueInfo      | type       | description |
| -------------   | ---------  | ----------- |
| cost       | decimal| csv 的核减额       |
| csv_values       | decimal | csv 处理之前的付款金额       |
| handle_csv_values| decimal |     csv 核减后的付款金额   |
| rebate_values | decimal   | 核减前的返点值 |
| handle_rebate_values| json arrau  | 核减后的返点值 |

返点计算流程（单个 account_id 内的）
### `RebateAccountSettleInfo`

| Field         | type      | description                                | unique  | index     | Null    |
| ------------- | --------- | -------------------------------------------| ------- | --------- | ------- |
| settle_season_id    | interger    |         返点结算 id，主键             | no      | yes       | no      |
| account_id        | varchar(50)    |          广告账户， 主键             | no      | yes       | no      |
| account_status        | integer   |          广告账户状态                | no      | yes       | no      |
| contract_id        | interger    |                                      | no      | yes       | no      |
| contract_name      | varchar(50)    |                                   | no      | yes       | no      |
| item              |  json dict      |       合同信息                    | no      | yes        | no     |
| total             | decimal         |         流水信息               | no      | yes        | no     |
| pre_settle_info  | PreSettleInfo         |      预返点信息               | no      | yes        | no     |
| median           | decimal         |     total 经过 Pre 计算后中间值        | no      | yes        | no     |
| settle_info      | SettleInfo         |         返点信息               | no      | yes        | no     |
| amount            | decimal         |         最终返点额度               | no      | yes        | no     |
| created       | datetime           | 创建时间                           | no      | yes       | no      |
| updated       | datetime           | 更新时间                           | no      | no        | no      |

RetbateType 为 facebook 时：

| PreSettleInfo      | type       | description |
| -------------   | ---------  | ----------- |
| increases       | json array | 核增项       |
| decreases       | json array | 核减项       |
| flag            | int        | 是否有核增减 |
| revenue_total   | decimal    | 封户判断后的流水|
| deduct_reset_revenue | integer   | 0 流水置为 0，1 取消变更 |
| deduct_reset_forfeit | integer   | 0 罚金置为 0，1 取消变更  |
| forfeit    | decimal   | 罚金  |
| coupon           | dict   | 优惠券额度 { 'sum':0, 'single': []}   |
| second_increases       | json array | 核增项       |
| second_decreases       | json array | 核减项       |
| second_flag            | int        | 是否有核增减 |

increases
{increases:[{"name": "ceshi ", "summary": "0.1"}, {"name": "ceshi01", "summary": "0.1"}]}

| SettleInfo       | type       | description |
| -------------   | ---------  | ----------- |
| increases       | json array | 提交前核增项       |
| decreases       | json array | 提交前核减项       |

RebateType 为 adwords_dvip 时：

| PreSettleInfo       | type       | description |
| -------------   | ---------  | ----------- |
| increases       | json array | 核增项       |
| decreases       | json array | 核减项       |
| revenue_total   | decimal    | 封户判断后的流水|
| deduct_reset_revenue | integer   | 0 流水置为 0，1 取消变更  |
| url              | file_url   | 上传 csv 的 url  |


RebateType 为 adwords_psp 时：

| PreSettleInfo       | type       | description |
| -------------   | ---------  | ----------- |
| increases       | json array | 核增项       |
| decreases       | json array | 核减项       |
| revenue_total   | decimal    | 封户判断后的流水|


| SettleInfo       | type       | description |
| -------------   | ---------  | ----------- |
| increases       | json array | 提交前核增项       |
| decreases       | json array | 提交前核减项       |





