
### 权限管理设计方案

#### Company

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---
company_id|integer|公司 ID，主键|yes|yes|no|
category|integer|公司类型：1 为 Internal, 2 为 UA Vendor, 3 为 External_Advertiser, 4 为 settlement 对应的公司|no|yes|no|
alias|varchar(50)|公司别称，唯一|yes|yes|no|
users|Json|用户ID列表|no|no|yes|
legal_name|varchar(100)|公司名称|no|yes|no|
fraud_settings|json dict|fraud 配置|no|no|no|
account_admin|string|ua vendor 的管理员账号(deprecated)|no|no|yes|
bank_info|string|company network 名称|no|no|yes|
status|integer|状态：1 为 enabled,2 为 disabled|no|yes|no|
match_name|json| 抓取时用到的名字                                             |no|no|yes|
buying_side|integer|区分广告主和优化师团队|no|no|yes|
creator|varchar(50)|公司的创建人 email|no|yes|no|
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

#### Organization

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
org_id|integer|部门ID, 主键|yes|yes|no|
superior_org_id|integer|父级组织 ID|no|yes|yes|
category|integer|部门分类：1 为 Internal Advertiser，2 为 MB Consulting Team，3 为 MB Agency Team，4 为 UA Department，5 为 Finance, 6 为 Administrator|no|yes|no|
name|varchar(50)|部门名称|no|yes|no|
company_id|integer|公司 ID|no|yes|yes|
company_alias|varchar(50)|公司别称|no|yes|yes|
visibility|array|product team 的 ID 列表。为空的时候表示 all|no|yes|yes|
status|integer|状态：1 为 enabled,2 为 disabled|no|yes|no|
creator|varchar(50)|部门的创建人 email|no|yes|no|
offer_effective_date_limit|int||no|yes|no|
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

联合唯一索引：category, name

#### User

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
user_id|int|用户id, 主键|no|yes|no|
email|varchar(50)|邮箱地址|no|yes|no|
name|varchar(50)|用户的名称|no|yes|no|
optimizer_id|varchar(50)|优化师ID|no|yes|yes|
status|int|状态：1 为 enabled,2 为 disabled|no|yes|no|
creator|varchar(50)|用户的创建者的email|no|yes|no|
created|datetime|created time|no|yes|no|
updated|datetime|updated time|no|yes|no|

#### UserResource

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
email|varchar(50)|邮箱地址, 主键|no|yes|no|
resource_type|integer|资源类型, 主键|no|yes|no|
resource_ids|json array|数据ID列表|no|no|yes|

#### Role

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
role_id|integer|角色ID 主键|yes|yes|no|
company_id|integer|所属公司的ID|no|yes|yes|
org_id|integer|所属部门的ID|no|yes|yes|
name|varchar(50)|角色名称|no|yes|no|
creator|varchar(50)|角色的创建人 email|no|yes|no|
modules|json array|页面权限列表|no|no|yes|
actions|json array|操作权限列表|no|no|yes|
resources|json array|通用数据权限列表|no|no|yes|
status|integer|状态：1 为 enabled,2 为 disabled|no|yes|no|
updated|datetime|更新时间|no|yes|no|
created|datetime|created time|no|yes|no|

#### UserRole

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---
user_id|varchar(50)|邮箱地址, 主键|no|yes|no|
role_id|integer|角色ID, 主键|yes|yes|no|
created|datetime|created time|no|yes|no|


### Dashboard

#### RoleView

| Field      | type      | description      | unique | index | Null |
| ---------- | --------- | ---------------- | ------ | ----- | ---- |
| role_id    | integer   | 角色 ID, 主键         | no     | yes   | no   |
| view_id    | integer   | view ID, 主键         | no     | yes   | no   |
| raw_data   | boolean   | 能否下载原始数据 | no     | yes   | no   |
| dimension | json | 默认筛选权限     | no     | yes   | no   |
| created    | datetime  | 创建时间         | no     | yes   | no   |
| updated    | datetime  | 更新时间         | no     | no    | no   |

####  ViewModel

| Field         | type     | description           | default | index |
| ------------- | -------- | --------------------- | ------- | ----- |
| view_id       | integer  | 表格 id               |         | yes   |
| view_name     | string   | 表格 标题             |         | yes   |
| view_category | string   | mode or asset         | mode    | no    |
| mode_view_id  | string   | 对应mode report的id   | ''      | yes   |
| dimensions    | json     | list of dimension ids | []      | no    |
| created       | datetime |                       |         | yes   |
| updated       | datetime |                       |         | yes   |

#### DimensionModel

| Field          | type     | description                                                  | default                       | index |
| -------------- | -------- | ------------------------------------------------------------ | ----------------------------- | ----- |
| dimension_id   | integer  |                                                              |                               | yes   |
| dimension_name | string   |                                                              |                               | yes   |
| mode_name      | string   | dimension name in mode report                                | null                          | yes   |
| default_value  | string   | 默认值: \_\_invalid\_place\_holder\_\_                       | _\_invalid\_place\_holder\_\_ | no    |
| template       | json     | 模板列表                                                     | []                            | no    |
| asset_name     | string   | 在top asset中的维度名称                                      | null                          | no    |
| fields         | json     | 从数据库读出的数据的format, 如['id', 'name']<br />是指读出的数据格式是{id:  XXX, name: YYY} | [id, name]                    | no    |
| primary_field  | string   |                                                              | id                            | no    |
| created        | datetime |                                                              |                               | yes   |
| updated        | datetime |                                                              |                               | yes   |



### Account Management

#### PayeeAccountModel

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
media_account_id|integer|主键|no|yes|no|
media|varchar(50)|账户投放平台|no|yes|no|
account_id|varchar(100)|账户 ID|no|yes|no|
account_name|varchar(100)|我们自己添加的账户标志|no|no|yes|
agency_type|varchar(12)|opua, outsource|no|no|no|
payee|varchar(50)|资金最终的收款方，opua 里指的是 agency|no|yes|no|
default_payee|varchar(100)|ihandy 的直接收款方|no|yes|yes|
bank_info|varchar(100)||no|yes|yes|
credit_card|integer|绑定信用卡 cherrypie 里的账号|no|yes|yes|
card_id|varchar(100)|绑定信用卡的账号|no|no|yes|
updated|datetime|内审更新时间|no|no|no|
created|datetime|创建时间|no|no|no|
