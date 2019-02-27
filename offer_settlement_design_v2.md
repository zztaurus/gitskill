### API

#### 获取报表列表

```
GET /orgs/<org_id>/reports
```

请求参数：

| Name        | Type    | Required | Default Value | Description                                   |
| ----------- | ------- | -------- | ------------- | --------------------------------------------- |
| page        | integer | no       | 1             | 页号                                          |
| per_page    | integer | no       | 10            | 每页条数                                      |
| order_by    | string  | no       | 排序规则      |                                               |
| filter_by   | string  | no       |               | 筛选                                          |
| distinct_by | string  | no       |               | distinct_by 不为空，page 和 per_page 参数失效 |
| csv_title   | list    | no       |               | 导出的 CSV 的表头                             |

请求示例：

```
GET /orgs/<org_id>/reports?distinct_by=org_name:085
GET /orgs/<org_id>/reports
```

返回结果：

```
Status: 200 OK
[#返回结果为 list，每个元素均为 Reporting 中 distict_by 名称对应的值
    ...
]

Status: 200 OK
{
  "reports": [
	{ # 参见 ReportInfo
	  "report_id": "",
	  "item_id": "",
	  "item_name": "",
	  "offer_id": "",
	  "offer_type": 1/2,
	  "offer_media": "",
	  "product_id": "",
	  "product_name": "",
	  "org_id": "",
	  "org_name": "",
	  "company_id": "",
	  "company_name": "",
	  "company_category": "",
	  "summary": xx,
	  "status": "",
	  "status_info": {},
	  "supporting": [],
	  "updated": "",
	  "created": "",
    },
	...
],
"page": ,
"per_page": ,
"total": ,
}
```

#### 获取报表详情

```
GET /orgs/<org_id>/reports/<report_id>
```

返回结果：

```
Status: 200 OK
{ # 参见 ReportInfo
  "item_id": "",
  "report_month": "",
  "item_name": "",
  "offer_id": "",
  "offer_type": "",
  "offer_media": "",
  "product_id": "",
  "product_name": "",
  "org_id": "",
  "org_name": "",
  "company_id": "",
  "company_name": "",
  "company_category": "",
  "increases": [{ # 参见 Increase
    "name": "",
    "summary": "",
  }...],
  "decreases": [{ # 参见 Decrease
    "name": "",
    "summary": "",
  }...],
  "summary": xx,
  "status": "",
  "status_info": [{ # 参见 StatusInfo
    "created": "",
    "email": "",
    "action": "",
    "comment": ""
  }...],
  "supporting": [{ # 参见 SupporInfo
    "name": "",
    "url": "",
  }...],
  "updated": "",
  "created": "",
}
```

StatusInfo

| Name    | Type   | Required | Default Value | Description |
| ------- | ------ | -------- | ------------- | ----------- |
| created | string | yes      |               | 创建时间    |
| email   | string | yes      |               | 邮箱地址    |
| action  | string | yes      |               | 动作        |
| comment | string | yes      |               | 评论        |

#### 获取报表基础数据

```
GET /orgs/<org_id>/reports/<report_id>/records
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |

返回结果：

```
Status: 200 OK
{
  "records":[
    { # 参见 ReportDataInfo
      "create_date": "",
      "product_name": "",
      "media": "",
      "country": "",
      "install": ,
      "optimizer": "",
      "impression": ,
      "click": ,
      "spent": ,
      "purchase": ,
      "ctr": ,
      "cvr": ,
      "ppi": ,
      "cpi": ,
      "cpm": ,
      "created": xx,
  },
  ...
],
"page": ,
"per_page": ,
"total": ,
}
```

#### 获取报表基础留存数据

```
GET /orgs/<org_id>/reports/<report_id>/retentions
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |

返回结果：

```
Status: 200 OK
{
  "records":[
    { # 参见 ReportRetentionInfo
      "create_date": "",
      "product_name": "",
      "media": "",
      "country": "",
      "install": ,
      "retention_day_1": ,
      "retention_install": ,
  },
  ...
],
"page": ,
"per_page": ,
"total": ,
```

  }

#### 上传报表文件

```
POST /orgs/<org_id>/reports/<report_id>/files/<file_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
| file | File | yes      |               | 文件流      |

返回结果：

```
Status: 200 OK
{
  "file_name": "",
  "file_type": "",
  "url": "http://xxxx"
}
```

#### 添加报表依赖信息

```
POST /orgs/<org_id>/reports/<report_id>/extra
```

请求参数：

| Name       | Type             | Required | Default Value | Description |
| ---------- | ---------------- | -------- | ------------- | ----------- |
| increases  | list Increase    | no       |               | 添加项      |
| decreases  | list Decrease    | no       |               | 删减项      |
| supporting | list SupportInfo | no       |               | 说明        |

Increase/Decrease

| Name    | Type    | Required | Default Value | Description |
| ------- | ------- | -------- | ------------- | ----------- |
| name    | string  | yes      |               | 名称        |
| summary | decimal | yes      |               | 总价        |

SupportInfo

| Name      | Type   | Required | Default Value | Description |
| --------- | ------ | -------- | ------------- | ----------- |
| file_name | string | yes      |               | 文件名称    |
| file_type | string | yes      |               | 文件类型    |
| url       | Url    | yes      |               | 文件路径    |

返回结果：

```
Status: 200 OK
```

#### 提交待审核的报表

```
PUT /orgs/<org_id>/reports/<report_id>/submit
```

返回结果：

```
Status: 200 OK
```

#### review 报表

```
PUT /orgs/<org_id>/reports/<report_id>/review
```

请求参数：

| Name    | Type   | Required | Default Value | Description |
| ------- | ------ | -------- | ------------- | ----------- |
| comment | string | no       |               | 备注        |

返回结果：

```
Status: 200 OK
```

#### 再次 review 报表

```
PUT /orgs/<org_id>/reports/<report_id>/review2
```

请求参数：

| Name    | Type   | Required | Default Value | Description |
| ------- | ------ | -------- | ------------- | ----------- |
| comment | string | no       |               | 备注        |

返回结果：

```
Status: 200 OK
```

#### review 通过报表

```
PUT /orgs/<org_id>/reports/<report_id>/passed
```

请求参数：

| Name    | Type   | Required | Default Value | Description |
| ------- | ------ | -------- | ------------- | ----------- |
| comment | string | yes      |               | 备注        |

返回结果：

```
Status: 200 OK
```

#### review 拒绝报表

```
PUT /orgs/<org_id>/reports/<report_id>/rejected
```

请求参数：

| Name    | Type   | Required | Default Value | Description |
| ------- | ------ | -------- | ------------- | ----------- |
| comment | string | yes      |               | 备注        |

返回结果：

```
Status: 200 OK
```

#### 第三次review 报表

```
PUT /orgs/<org_id>/reports/<report_id>/review3
```

请求参数：

| Name    | Type   | Required | Default Value | Description |
| ------- | ------ | -------- | ------------- | ----------- |
| comment | string | yes      |               | 备注        |

返回结果：

```
Status: 200 OK
```

#### 第二次pass通过报表

```
PUT /orgs/<org_id>/reports/<report_id>/passed2
```

请求参数：

| Name    | Type   | Required | Default Value | Description |
| ------- | ------ | -------- | ------------- | ----------- |
| comment | string | yes      |               | 备注        |

返回结果：

```
Status: 200 OK
```

### Model

#### SettlementOfOffer

| field                     | type             | description                                                  | unique | index | NULL |      |
| ------------------------- | ---------------- | ------------------------------------------------------------ | ------ | ----- | ---- | ---- |
| report_id                 | varchar(100)     | yes                                                          | yes    | no    |      |      |
| report_month              | varchar(10)      | 主键                                                         | yes    | yes   | no   |      |
| source                    | varchar(128)     |                                                              | no     | yes   | no   |      |
| offer_id                  | varchar(10)      | Offer 的 ID                                                  | no     | yes   | no   |      |
| offer_type                | integer          | 分类：1 代表 task,2 代表 order                               | no     | yes   | no   |      |
| offer_version             | integer          | no                                                           | yes    | no    |      |      |
| product_id                | integer          | 产品 ID                                                      | no     | yes   | no   |      |
| product_name              | varchar(32)      | 产品内部名称                                                 | no     | yes   | no   |      |
| product_info              | json             | no                                                           | no     | no    |      |      |
| org_id                    | integer          | 组织 ID                                                      | no     | yes   | no   |      |
| org_name                  | varchar(50)      | 组织名称                                                     | no     | yes   | no   |      |
| org_category              | integer          | no                                                           | no     | no    |      |      |
| consumer_org_id           | integer          | 产品投放的组织 ID                                            | no     | yes   | yes  |      |
| consumer_org_name         | varchar(50)      | 产品投放的组织名称                                           | no     | yes   | no   |      |
| consumer_org_category     | integer          | no                                                           | no     | yes   |      |      |
| consumer_company_id       | integer          | 公司 ID                                                      | no     | yes   | no   |      |
| consumer_company_name     | varchar(50)      | 公司名称                                                     | no     | yes   | no   |      |
| consumer_company_category | integer          | 公司类型：1 为 internal                                      | no     | yes   | no   |      |
| media                     | list string      | 投放平台列表                                                 | no     | no    | no   |      |
| sub_media                 | list string      | 投放平台列表                                                 | no     | no    | no   |      |
| effective_date            | date             | no                                                           | yes    | no    |      |      |
| expiration_date           | date             | no                                                           | yes    | no    |      |      |
| item_name                 | varchar(500)     | item 名称                                                    | no     | yes   | no   |      |
| regions                   | json list string | 国家列表                                                     | no     | no    | no   |      |
| languages                 | json list string | 语言列表                                                     | no     | no    | yes  |      |
| daily_budget              | json dict        |                                                              | no     | no    | yes  |      |
| daily_install             | json dict        | 每日安装量目标范围                                           | no     | no    | yes  |      |
| daily_cpi                 | json dict        | 阶梯价                                                       | no     | no    | yes  |      |
| kpi_by_retention          | json dict        | 阶梯 kpi                                                     | no     | no    | yes  |      |
| kpi_decrease              | real             |                                                              | no     | no    | no   |      |
| increases                 | json array       | 增项列表                                                     | no     | no    | yes  |      |
| decreases                 | json array       | 减项列表                                                     | no     | no    | yes  |      |
| manual_creases            | real             |                                                              | no     | no    | no   |      |
| total_spend               | real             | 所有花费                                                     | no     | no    | no   |      |
| total                     | decimal          |                                                              | no     | no    | yes  |      |
| summary                   | decimal          | 主要花费                                                     | no     | yes   | no   |      |
| amount                    | decimal          |                                                              | no     | yes   | no   |      |
| credit_card_cost          | real             | 信用卡花费                                                   | no     | no    | no   |      |
| status                    | integer          | 状态：1 为 Draft,2 为 Draft(Modified),3 为 PendingLeaderReview,4 为 PendingProductTeamReview,5 为 Draft(Reject),6 为 Closed | no     | yes   | no   |      |
| status_info               | json dict        | 状态信息                                                     | no     | no    | yes  |      |
| supporting                | json array       | 支持文档信息                                                 | no     | no    | yes  |      |
| extra                     | json dict        |                                                              | no     | no    | yes  |      |
| updated                   | datetime         | 更新时间                                                     | no     | no    | no   |      |
| created                   | datetime         | 创建时间                                                     | no     | yes   | no   |      |

#### MetricsOfCampaign

| field             | type         | description | unique | index | NULL |      |
| ----------------- | ------------ | ----------- | ------ | ----- | ---- | ---- |
| create_date       | datetime     |             | no     | yes   | no   |      |
| campaign_id       | varchar(128) |             | no     | yes   | no   |      |
| media             | varchar(128) | 投放平台    | no     | yes   | no   |      |
| country           | varchar(128) | 国家        | no     | yes   | no   |      |
| account_id        | varchar(128) | no          | yes    | no    |      |      |
| platform          | varchar(128) | no          | yes    | no    |      |      |
| app_id            | varchar(128) |             | no     | yes   | no   |      |
| app_name          | varchar(128) |             | no     | yes   | no   |      |
| agency_type       | varchar(128) |             | no     | yes   | no   |      |
| store             | varchar(128) |             | no     | yes   | no   |      |
| store_link        | varchar(500) |             | no     | yes   | no   |      |
| payee             | varchar(128) |             | no     | yes   | no   |      |
| campaign_name     | varchar(300) |             | no     | yes   | no   |      |
| optimizer_company | varchar(128) |             | no     | yes   | no   |      |
| optimizer_team    | varchar(128) |             | no     | yes   | yes  |      |
| optimizer_group   | varchar(128) |             | no     | yes   | yes  |      |
| optimizer         | varchar(128) |             | no     | yes   | yes  |      |
| reaches           | big integer  |             | no     | no    | no   |      |
| installs          | big integer  | 安装数      | no     | no    | no   |      |
| impressions       | big integer  |             | no     | no    | no   |      |
| clicks            | big integer  | 点击数      | no     | no    | no   |      |
| spent             | double       |             | no     | no    | no   |      |
| return_value      | double       |             | no     | no    | no   |      |
| purchase          | double       |             | no     | no    | no   |      |
| ctr               | double       |             | no     | no    | no   |      |
| cvr               | double       |             | no     | no    | no   |      |
| ppi               | double       |             | no     | no    | no   |      |
| cpi               | double       |             | no     | no    | no   |      |
| cpm               | double       |             | no     | no    | no   |      |
| created           | datetime     | 创建时间    | no     | yes   | no   |      |
| updated           | datetime     | 更新时间    | no     | no    | no   |      |

联合主键：create_date, campaign_id, media, country

#### SettlementProcessRecord

| field                     | type        | description                                    | unique | index | NULL |      |
| ------------------------- | ----------- | ---------------------------------------------- | ------ | ----- | ---- | ---- |
| month                     | varchar(10) | 主键,结算的月份                                | yes    | yes   | no   |      |
| month_crawl_status        | integer     | datahome每月抓取是否完成， 0为未完成， 1为完成 | no     | yes   | no   |      |
| settlement_process_status | integer     | cherrypie 同步是否完成，0为未完成， 1为完成    | no     | yes   | no   |      |
| updated                   | datetime    | 更新时间                                       | no     | yes   | no   |      |
| created                   | datetime    | 创建时间                                       | no     | yes   | no   |      |

