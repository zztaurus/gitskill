## dock_console

### Account

#### Account

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
email|string|邮件地址，主键|yes|yes|no|
password|string|密码|no|yes|no|
status|integer|状态：1 为 enabled,2 为 disabled|no|yes|no|
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

### company
#### Company

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
company_id|integer|公司 ID，主键|yes|yes|no|
category|integer|公司类型：1 为 Internal, 2 为 UA Vendor, 3 为 External_Advertiser, 4 为 settlement 对应的公司|no|yes|no|
alias|varchar(50)|公司别称，唯一|yes|yes|no|
legal_name|varchar(100)|公司名称，唯一|no|yes|no|
business_development|list email|bd 的列表|no|no|yes|
account_manager|list email|am 的列表|no|no|yes|
account_admin|string|ua vendor 的管理员账号|no|no|yes|
fraud_settings|json dict|fraud 配置|no|no|no|
bank_info|string|company network 名称|no|no|yes|
status|integer|状态：1 为 enabled,2 为 disabled|no|yes|no|
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

### org
#### Organization

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
org_id|integer|组织 ID, 主键|yes|yes|no|
category|integer|组织分类：1 为 Internal Advertiser，2 为 MB Consulting Team，3 为 MB Agency Team，4 为 UA Department，5 为 Finance, 6 为 Administrator|no|yes|no|
name|varchar(100)|组织名称|yes|yes|no|
company_id|integer|公司 ID|no|yes|yes|
company_alias|varchar(50)|公司别称|no|yes|yes|
default_leader|varchar(50)|leader 邮箱|no|yes|yes|
visibility|array|product team 的 ID 列表。为空的时候表示 all|no|yes|yes|
functions|array|组织所具有的功能列表|no|yes|yes|
status|integer|状态：1 为 enabled,2 为 disabled|no|yes|no|
offer_effective_date_limit|int||no|yes|no|
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

联合唯一索引：category, name

### role
#### Role

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
role_id|integer|role id|yes|yes|no|
name|varchar(50)|role alias|no|no|no|
permissions|json array|权限列表|no|no|yes|
description|text|description|no|no|no|
created|datetime|created time|no|yes|no|

#### OrgRole

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
role_id|integer|role id|no|yes|no|
org_category|integer||no|yes|no|
created|datetime|created time|no|yes|no|

联合主键：org_category, role_id

### user
#### UserRole
field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
email|varchar(50)|邮箱地址|no|yes|no|
org_id|integer|组织 ID|no|yes|no|
role_id|int|role id|no|yes|no|
is_default|boolean|是否是默认角色|no|no|no|
is_leader|boolean|是否是 leader|no|no|yes|
status|int|状态：1 为 enabled,2 为 disabled|no|yes|no|
created|datetime|created time|no|yes|no|
updated|datetime|updated time|no|yes|no|

联合主键：org_id, email

#### UserPermisson

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
org_id|int|role id|yes|yes|no|
email|varchar(50)|role id|no|yes|no|
action|varchar(50)| |no|yes|no|
resource|varchar(50)||no|yes|no|
created|datetime|created time|no|no|no|
updated|datetime|created time|no|no|no|

联合主键：org_id, email, action, resource

## dock_offer
### audittrail
#### AuditTrail

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
trail_id|integer|主键|yes|yes|no|
email|varchar(50)|邮箱地址|no|yes|no|
before|json dict|修改之前|no|no|yes|
after|json dict|修改之后|no|no|yes|
description|text|备注|no|no|yes|
created|datetime|创建时间|no|yes|no|

### offer
#### Offer

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|
offer_id|varchar(10)|主键|yes|yes|no|
offer_type|integer|分类：1 代表 task,2 代表 order|no|yes|no|
product_id|integer|产品 ID|no|yes|no|
product_name|varchar(50)|产品内部名称|no|yes|no|
product_info|json|产品信息|no|no|no|
org_id|integer|组织 ID|no|yes|no|
org_name|varchar(50)|组织名称|no|yes|no|
org_category|integer|组织类型|no|no|no|
company_id|integer|公司 ID|no|yes|yes|
company_name|varchar(50)|公司名称|no|yes|yes|
company_category|integer|公司类型：1 为 internal, 2 为 UA Vendor, 3 为 External Advertiser|no|yes|yes|
consumer_org_id|integer|产品投放的组织 ID|no|yes|no|
consumer_org_name|varchar(50)|产品投放的组织名称|no|yes|no|
consumer_org_category|integer|组织类型|no|no|no|
consumer_company_id|integer|产品投放的公司 ID|no|yes|yes|
consumer_company_name|varchar(50)|产品投放的公司名称|no|yes|yes|
consumer_company_category|integer|产品投放的公司类型：1 为 internal|no|yes|yes|
optimizers|json list email||no|no|yes|
business_development|json list email||no|no|yes|
version_status|integer||no|yes|yes|
media|json array string|投放平台列表|no|no|no|
sub_media|json array string json|投放平台列表|no|no|no|
effective_date|date|生效日期|no|yes|no|
expiration_date|date|截止日期|no|no|yes|
notes|json dict|说明|no|no|no|
items|json array dict||no|no|yes|
status|integer|状态：1 为 Running,2 为 Stopped|no|yes|no|
current_version|integer|当前版本|no|no|yes|
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

#### OfferVersion

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
offer_id|varchar(10)|offer 的 ID，和 offer_version 组成联合主键|no|yes|no|
offer_version|integer|offer 的版本|no|yes|no|
offer_type|integer|分类：1 代表 task,2 代表 order|no|yes|no|
source|varchar(10)|渠道：opua,outsource|no|yes|no|
product_id|integer|产品 ID|no|yes|no|
product_name|varchar(50)|产品内部名称|no|yes|no|
product_info|json|产品信息|no|no|no|
org_id|integer|组织 ID|no|yes|no|
org_name|varchar(50)|组织名称|no|yes|no|
org_category|integer|组织类型|no|no|no|
company_id|integer|公司 ID|no|yes|yes|
company_name|varchar(50)|公司名称|no|yes|yes|
company_category|integer|公司类型：1 为 internal|no|yes|yes|
media|list string json|投放平台列表|no|no|no|
sub_media|list string json|投放平台列表|no|no|no|
effective_date|date|生效日期|no|no|no|
expiration_date|date|截止日期|no|no|yes|
expect_expiration_date|date|期望截止日期|no|no|yes|
notes|json dict|说明|no|no|no|
items|json array dict||no|no|yes|
status|integer|状态：1 为 Created,2 为 PendingLeaderReview,3 为 PendingProductTeamReview,4 为 Enabled,5 为 Rejected|no|yes|no|
extra|json dict||no|no|yes|
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

### optimizer

#### Optimizer

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
optimizer_id|integer|优化师主键 |yes|yes|no|
org_id|integer|组织 ID|no|yes|no|
email|varchar(32)|优化师邮箱|no|yes|no|
status|int|状态：1 为 enabled,2 为 disabled|no|yes|no|
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

#### OptimizerGroup

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
group_id|integer| 主键 |yes|yes|no|
org_id|integer|组织 ID|no|yes|no|
name|varchar(32)|组织名称|yes|yes|no|
department_leader|varchar(100)|department_leader|no|yes|yes|
status|int|状态：1 为 enabled,2 为 disabled|no|yes|no|
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

联合唯一索引：org_id, namfraud_settingse

#### OptimizerGroupMap

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
group_id|integer| 组 ID |no|yes|no|
optimizer_id|integer|优化师 ID |no|yes|no|
is_leader|boolean|是否是 leader |no|yes|no|

联合主键：group_id, optimizer_id


### Product

#### Product

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
product_id|integer|主键|yes|yes|no|
org_id|integer|组织 ID|no|yes|no|
company_id|integer|公司 ID|no|yes|no|
company_name|varchar(50)|公司名称|no|yes|no|
company_category|integer|公司类型：1 为 internal, 2 为 UA Vendor, 3 为 External Advertiser|no|yes|no|
internal_name|varchar(50)|内部名称|yes|yes|no|
store|integer|商店类型：1 为 GooglyPlay，2 为 AppStore|no|yes|no
running_offer_count|integer||no|no|no|
bundle_id|varchar(100)||no|yes|no|
apple_id|varchar(20)||no|yes|no|
store_link|varchar(200)||no|no|no|
support_device|varchar(20)||no|no|yes|
min_os_version|varchar(100)||no|no|yes|
appsflyer_id|varchar(100)||no|yes|yes|
facebook_id|varchar(20)||no|yes|yes|
fackbook_fanpage|varchar(100)||no|yes|yes|
product_manager|json list email||no|no|no|
status|integer|状态：1 为 enabled,2 为 disabled|no|yes|no|
updated|datetime|更新时间|no|no|no|
created|datetime|创建时间|no|yes|no|

#### SettlementProcessRecord

| field                     | type        | description                                    | unique | index | NULL |      |
| ------------------------- | ----------- | ---------------------------------------------- | ------ | ----- | ---- | ---- |
| month                     | varchar(10) | 主键,结算的月份                                | yes    | yes   | no   |      |
| month_crawl_status        | integer     | datahome每月抓取是否完成， 0为未完成， 1为完成 | no     | yes   | no   |      |
| settlement_process_status | integer     | cherrypie 同步是否完成，0为未完成， 1为完成    | no     | yes   | no   |      |
| updated                   | datetime    | 更新时间                                       | no     | yes   | no   |      |
| created                   | datetime    | 创建时间                                       | no     | yes   | no   |      |

### region

#### RegionGroup

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
group_id|integer| 主键 |yes|yes|no|
org_id|integer|组织 ID|no|yes|no|
group_name|varchar(32)|组织名称|yes|yes|no|
regions|list string|列表|no|no|no|
product_id|integer|region 属于这个 App|no|yes|no|
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

### reporting
#### Reporting

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
report_id|varchar(100)|yes|yes|no|
report_month|varchar(10)|主键|yes|yes|no|
channel|varchar(128)||no|yes|no|
offer_id|varchar(10)|Offer 的 ID|no|yes|no|
offer_type|integer|分类：1 代表 task,2 代表 order|no|yes|no|
offer_version|integer|no|yes|no|
product_id|integer|产品 ID|no|yes|no|
product_name|varchar(32)|产品内部名称|no|yes|no|
product_info|json|no|no|no|
org_id|integer|组织 ID|no|yes|no|
org_name|varchar(50)|组织名称|no|yes|no|
org_category|integer|no|no|no|
consumer_org_id|integer|产品投放的组织 ID|no|yes|yes|
consumer_org_name|varchar(50)|产品投放的组织名称|no|yes|no|
consumer_org_category|integer|no|no|yes|
consumer_company_id|integer|公司 ID|no|yes|no|
consumer_company_name|varchar(50)|公司名称|no|yes|no|
consumer_company_category|integer|公司类型：1 为 internal|no|yes|no|
media|list string|投放平台列表|no|no|no|
sub_media|list string|投放平台列表|no|no|no|
effective_date|date|no|yes|no|
expiration_date|date|no|yes|no|
item_name|varchar(500)|item 名称|no|yes|no|
regions|json list string|国家列表|no|no|no|
languages|json list string|语言列表|no|no|yes|
daily_budget|json dict||no|no|yes|
daily_install|json dict|每日安装量目标范围|no|no|yes|
daily_cpi|json dict|阶梯价|no|no|yes|
kpi_by_retention|json dict|阶梯 kpi|no|no|yes|
increases|json array|增项列表|no|no|yes|
decreases|json array|减项列表|no|no|yes|
total|decimal||no|no|yes|
summary|decimal|主要花费|no|yes|no|
amount|decimal||no|yes|no|
status|integer|状态：1 为 Draft,2 为 Draft(Modified),3 为 PendingLeaderReview,4 为 PendingProductTeamReview,5 为 Draft(Reject),6 为 Closed|no|yes|no|
status_info|json dict|状态信息|no|no|yes|
supporting|json array|支持文档信息|no|no|yes|
extra|json dict||no|no|yes|
updated|datetime|更新时间|no|no|no|
created|datetime|创建时间|no|yes|no|

#### UaVendorAccountSetting

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
payee|varchar(100)|no|yes|yes|
media|varchar(100)||no|no|yes|
account_id|varchar(100)||no|no|yes|
updated|datetime|更新时间|no|no|no|
created|datetime|创建时间|no|yes|no|

联合主键：payee, media, account_id

#### PayeeMediaAgency

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
media|varchar(100)||no|no|yes|
agency|varchar(100)||no|no|yes|
media_source|varchar(50)||no|yes|no|
payee|varchar(100)|no|yes|yes|
updated|datetime|更新时间|no|no|no|
created|datetime|创建时间|no|yes|no|

联合主键：media, agency, media_source, payee


#### MediaAccount

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
media|varchar(128)||no|no|yes|
adaccountid|varchar(128)||no|no|no|
agency|varchar(128)||no|yes|no|
name|varchar(118)|no|yes|no|
status|integer|状态：1 为 enabled,2 为 disabled|no|yes|no|
status_changed|datetime|状态变更时间|no|no|no|
punishment|decimal|罚金|no|no|yes|
updated|datetime|更新时间|no|no|no|
created|datetime|创建时间|no|yes|no|

联合主键：media, adaccountid

#### UACampaign

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
create_date|datetime||no|yes|no|
adaccountid|varchar(128)||no|yes|no|
campaign_id|varchar(128)||no|yes|no|
media|varchar(128)|投放平台|no|yes|no|
region|varchar(128)|国家|no|yes|no|
agency|varchar(128)|no|yes|no|
platform|varchar(128)|no|yes|no|
app_id|varchar(128)||no|yes|no|
app_name|varchar(128)||no|yes|no|
channel|varchar(128)||no|yes|no|
store|varchar(128)||no|yes|no|
store_link|varchar(128)||no|yes|no|
campaign_name|varchar(128)||no|yes|no|
optimizer_company|varchar(128)||no|yes|no|
optimizer_team|varchar(128)||no|yes|yes|
optimizer_group|varchar(128)||no|yes|yes|
optimizer|varchar(128)||no|yes|yes|
reach|big integer||no|no|no|
installs|big integer|安装数|no|no|no|
impressions|big integer||no|no|no|
clicks|big integer|点击数|no|no|no|
spent|double||no|no|no|
purchase|double||no|no|no|
ctr|double||no|no|no|
cvr|double||no|no|no|
ppi|double||no|no|no|
cpi|double||no|no|no|
cpm|double||no|no|no|
media_source_agency|json ||no|no|yes|
created|datetime|创建时间|no|yes|no|
updated|datetime|更新时间|no|no|no|

联合主键：create_date, adaccountid, campaign_id, media, region

#### UARetention

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
install_day|datetime||no|yes|no|
campaign_id|varchar(128)||no|yes|no|
app_id|varchar(128)||no|yes|no|
media_source|varchar(128)||no|yes|no|
agency|varchar(128)||no|yes|no|
country|varchar(128)|国家|no|yes|no|
channel|varchar(128)||no|yes|no|
app_name|varchar(128)||no|yes|no|
campaign_name|varchar(128)||no|yes|no|
optimizer_company|varchar(128)||no|yes|no|
optimizer_team|varchar(128)||no|yes|yes|
optimizer_group|varchar(128)||no|yes|yes|
optimizer|varchar(128)||no|yes|yes|
cost|decimal||no|no|no|
impressions|big integer||no|no|no|
clicks|big integer|点击数|no|no|no|
installs|big integer|安装数|no|no|no|
session|big integer||no|no|no|
retention_day_1|big integer||no|no|no|
retention_day_2|big integer||no|no|no|
retention_day_3|big integer||no|no|no|
retention_day_4|big integer||no|no|no|
retention_day_5|big integer||no|no|no|
retention_day_6|big integer||no|no|no|
retention_day_7|big integer||no|no|no|
created|datetime|创建时间|no|yes|no|
updated|datetime|更新时间|no|no|no|

联合主键：install_day, campaign_id, app_id, media_source, agency, country


### setting
#### Settings

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
key|varchar(32)|标志，主键|yes|yes|no
value|text|值|no|no|no
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

### todo
#### ToDo

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
todo_id|integer|主键|yes|yes|no|
email|varchar(50)|邮箱地址|no|yes|no|
detail|json|todo detail|no|yes|no|
message|text(200)|详细内容|no|no|yes|
offer_info|json|对应的 Offer 的版本信息|no|yes|yes|
reporting_info|json|对应的 reporting 的信息|no|yes|yes|
category|integer|1:message 2:todo 3:done|no|yes|yes|
status|integer|1: 未读 /2: 已读|no|no|no|
created|datetime||no|yes|no|
updated|datetime||no|yes|no|



#### UserOffer

| field   | type       | description     | unique | index | NULL |
| ------- | ---------- | --------------- | ------ | ----- | ---- |
| email   | integer    | role id         | no     | yes   | no   |
| offer   | json array | offer 列表       | no     | no    | yes  |
| org_id  | integer    | org id          | no     | yes   | no   |
| tag     | integer    | 标签，1 代表隐藏 | no     | yes   | no   |
| created | datetime   |                 | no     | yes   | no   |
| updated | datetime   |                 | no     | yes   | no   |

联合主键：email,org_id,tag
