###API

####获取BudgetPool列表

```http
GET /apps/<app_id>/budget_pool
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |

返回结果：

```json
Status: 200 OK
{
    "budget_pool": [
        { 
          "budget_pool_id": "",
  		  "name": "",
  		  "tag": "",
  		  "lifetime_spend_type": "",
  		  "lifetime_spend_value": "",
  		  "daily_spend_type": "",
  		  "daily_spend_value: "",
  		  "start_date": "",
  		  "end_date": ""
        },
        ...
    ]
}
```

####获取指定BudgetPool

```http
GET /apps/<app_id>/budget_pools/<budget_pool_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |

返回结果：

```json
Status: 200 OK
{
    "budget_pool_id": "",
  	"name": "",
  	"tag": "",
  	"lifetime_spend_type": "",
  	"lifetime_spend_value": "",
  	"daily_spend_type": "",
  	"daily_spend_value: "",
  	"start_date": "",
  	"end_date": ""
}
```

#### 更新BudgetPool

```http
POST /apps/<app_id>/budget_pools/<budget_pool_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签        |

返回结果：

```json
Status: 200 OK
```

#### 添加BudgetPool

```http
POST /apps/<app_id>/budget_pool
```

请求参数：

| Name                 | Type   | Required | Default Value | Description |
| -------------------- | ------ | -------- | ------------- | ----------- |
| name                 | string | yes      |               | 名称        |
| tags                 | json   |          |               | 标签        |
| lifetime_spend_type  | string |          |               |             |
| lifetime_spend_value | string |          |               |             |
| daily_spend_type     | string |          |               |             |
| daily_spend_value    | string |          |               |             |
| start_date           | date   |          |               |             |
| end_date             | date   |          |               |             |
|                      |        |          |               |             |

返回结果：

```json
Status: 200 OK
{
  "budget_pool_id": "",
  "created": "",
}
```

####获取StrategyGroup列表

```http
GET /apps/<app_id>/strategy_group
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |

返回结果：

```json
Status: 200 OK
{
    "strategy_group": [
        { 
		...
        },
        ...
    ]
}
```

####获取指定StrategyGroup

```http
GET /apps/<app_id>/strategy_groups/<strategy_group_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |
|      |      |          |               |             |



返回结果：

```json
Status: 200 OK
{
   ...
}
```

#### 更新StrategyGroup

```http
POST /apps/<app_id>/strategy_groups/<strategy_group_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签        |

返回结果：

```json
Status: 200 OK
```

#### 添加StrategyGroup

```http
POST /apps/<app_id>/strategy_group
```

请求参数：

| Name               | Type   | Required | Default Value | Description |
| ------------------ | ------ | -------- | ------------- | ----------- |
| name               | string |          |               |             |
| tags               | json   |          |               |             |
| adaccount_id       | int    |          |               |             |
| time_zone          | string |          |               |             |
| bid_strategy       | string |          |               |             |
| bid_amount         | string |          |               |             |
| budget_pool_id     | int    |          |               |             |
| campaign_name_rule | string |          |               |             |
| adset_name_rule    | string |          |               |             |
| ad_name_rule       | string |          |               |             |
| generate_strategy  | list   |          |               |             |
| billing_event      | string |          |               |             |
| delivery_type      | string |          |               |             |
| optimization_goal  | string |          |               |             |
| conversion_window  | string |          |               |             |
| app_install_state  | string |          |               |             |
| daily_budget       | string |          |               |             |
| campaign_objective | string |          |               |             |

返回结果：

```json
Status: 200 OK
{
  "strategy_group_id": "",
  "created": "",
}
```

####获取Audience列表

```http
GET /apps/<app_id>/audience
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |



返回结果：

```json
Status: 200 OK
{
    "audience": [
        { 
          ...
        },
        ...
    ]
}
```

####获取指定Audience

```http
GET /apps/<app_id>/audiences/<audience_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |
|      |      |          |               |             |



返回结果：

```json
Status: 200 OK
{
	...
}
```

#### 更新Audience

```http
POST /apps/<app_id>/audiences/<audience_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签        |

返回结果：

```json
Status: 200 OK
```

#### 添加Audience

```http
POST /apps/<app_id>/audience
```

请求参数：

| Name            | Type   | Required | Default Value | Description |
| --------------- | ------ | -------- | ------------- | ----------- |
| name            | string |          |               |             |
| tags            | json   |          |               |             |
| location_id     | int    |          |               |             |
| age_id          | int    |          |               |             |
| language_id     | int    |          |               |             |
| gender          | string |          |               |             |
| birthday        | date   |          |               |             |
| ethnic_affinity | string |          |               |             |

返回结果：

```
Status: 200 OK
{
  "success": [],
  "repeat": []
}
```

####获取Location列表

```http
GET /apps/<app_id>/location
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |

返回结果：

```
Status: 200 OK
{
    "location": [
        { 
        ...
        },
        ...
    ]
}
```

####获取指定Location

```http
GET /apps/<app_id>/locations/<location_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |
|      |      |          |               |             |



返回结果：

```
Status: 200 OK
{
  ...
}
```

#### 更新Location

```http
POST /apps/<app_id>/locations/<location_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签        |

返回结果：

```
Status: 200 OK
```

#### 添加Location

```http
POST /apps/<app_id>/location
```

请求参数：

| Name               | Type   | Required | Default Value | Description |
| ------------------ | ------ | -------- | ------------- | ----------- |
| name               | string |          |               |             |
| tags               | json   |          |               |             |
| countries          | list   |          |               |             |
| excluded_countries | list   |          |               |             |
| location_type      | string |          |               |             |

返回结果：

```
Status: 200 OK
{
  "location_id": "",
  "created": ""
}
```

####获取Age列表

```http
GET /apps/<app_id>/age
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |

返回结果：

```
Status: 200 OK
{
    "age": [
        { 
          ...
        },
        ...
    ]
}
```

####获取指定Age

```http
GET /apps/<app_id>/ages/<age_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |
|      |      |          |               |             |

返回结果：

```
Status: 200 OK
{
    ...
}
```

#### 更新Age

```http
POST /apps/<app_id>/ages/<age_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签​        |

返回结果：

```
Status: 200 OK
```

#### 添加Age

```http
POST /apps/<app_id>/age
```

请求参数：

| Name    | Type   | Required | Default Value | Description |
| ------- | ------ | -------- | ------------- | ----------- |
| name    | string |          |               |             |
| tags    | json   |          |               |             |
| age_max | string |          |               |             |
| age_min | string |          |               |             |

返回结果：

```
Status: 200 OK
{
  "age_id": "",
  "created": "",
}
```

####获取Language列表

```http
GET /apps/<app_id>/language
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |

返回结果：

```
Status: 200 OK
{
    "language": [
        { 
          ...
        },
        ...
    ]
}
```

####获取指定Language

```http
GET /apps/<app_id>/languages/<language_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |
|      |      |          |               |             |

返回结果：

```
Status: 200 OK
{
    ...
}
```

#### 更新Language

```http
POST /apps/<app_id>/languages/<language_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签        |

返回结果：

```
Status: 200 OK
{
    ...
}
```

#### 添加Language

```http
POST /apps/<app_id>/language
```

请求参数：

| Name            | Type   | Required | Default Value | Description |
| --------------- | ------ | -------- | ------------- | ----------- |
| name            | string |          |               |             |
| tags            | json   |          |               |             |
| values          | list   |          |               |             |
| excluded_values | list   |          |               |             |

返回结果：

```
Status: 200 OK
{
  "language_id": "",
  "created": "",
}
```

####获取Context列表

```http
GET /apps/<app_id>/context
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |

返回结果：

```
Status: 200 OK
{
    "context": [
        { 
         ...
        },
        ...
    ]
}
```

####获取指定Context

```http
GET /apps/<app_id>/placements/<context_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |
|      |      |          |               |             |

返回结果：

```
Status: 200 OK
{
   ...
}
```

#### 更新Context

```http
POST /apps/<app_id>/placements/<context_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签​        |

返回结果：

```
Status: 200 OK
```

#### 添加Context

```http
POST /apps/<app_id>/context
```

请求参数：

| Name      | Type   | Required | Default Value | Description |
| --------- | ------ | -------- | ------------- | ----------- |
| name      | string |          |               |             |
| tags      | json   |          |               |             |
| device_id | int    |          |               |             |
|           |        |          |               |             |

返回结果：

```
Status: 200 OK
{
  "success": [],
  "repeat": []
}
```

####获取Devices列表

```http
GET /apps/<app_id>/devices
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |

返回结果：

```
Status: 200 OK
{
    "devices": [
        { 
         ...
        },
        ...
    ]
}
```

####获取指定Devices

```http
GET /apps/<app_id>/devices/<device_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |
|      |      |          |               |             |



返回结果：

```
Status: 200 OK
{
    ...
}
```

#### 更新Devices

```http
POST /apps/<app_id>/devices/<device_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签        |

返回结果：

```
Status: 200 OK
{
    ...
}
```

#### 添加Devices

```http
POST /apps/<app_id>/devices
```

请求参数：

| Name            | Type   | Required | Default Value | Description |
| --------------- | ------ | -------- | ------------- | ----------- |
| name            | string |          |               |             |
| tags            | int    |          |               |             |
| values          | list   |          |               |             |
| excluded_values | list   |          |               |             |

返回结果：

```
Status: 200 OK
{
  "device_id": "",
  "created": "",
}
```

####获取Creative列表

```http
GET /apps/<app_id>/creative
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |

返回结果：

```
Status: 200 OK
{
    "creative": [
        { 
         ...
        },
        ...
    ]
}
```

####获取指定Creative

```http
GET /apps/<app_id>/creatives/<creative_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |
|      |      |          |               |             |

返回结果：

```
Status: 200 OK
{
    ...
}
```

#### 更新Creative

```http
POST /apps/<app_id>/creatives/<creative_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签        |

返回结果：

```
Status: 200 OK
```

#### 添加Creative

```http
POST /apps/<app_id>/creative
```

请求参数：

| Name              | Type   | Required | Default Value | Description |
| ----------------- | ------ | -------- | ------------- | ----------- |
| name              | string |          |               |             |
| tags              | json   |          |               |             |
| creative_type     | string |          |               |             |
| image_id          | int    |          |               |             |
| video_id          | int    |          |               |             |
| body_id           | int    |          |               |             |
| headline_id       | int    |          |               |             |
| call_to_action_id | int    |          |               |             |
| ad_account_id     | int    |          |               |             |
| app_id            | int    |          |               |             |

返回结果：

```
Status: 200 OK
{
  "success": [],
  "repeat": []
}
```

####获取Headline列表

```http
GET /apps/<app_id>/headline
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |

返回结果：

```
Status: 200 OK
{
    "budget_pool": [
        { 
         ...
        },
        ...
    ]
}
```

####获取指定Headline

```http
GET /apps/<app_id>/headlines/<headline_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |
|      |      |          |               |             |

返回结果：

```
Status: 200 OK
{
    ...
}
```

#### 更新Headline

```http
POST /apps/<app_id>/headlines/<headline_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签​        |

返回结果：

```
Status: 200 OK
{
    ...
}
```

#### 添加Headline

```http
POST /apps/<app_id>/headline
```

请求参数：

| Name  | Type   | Required | Default Value | Description |
| ----- | ------ | -------- | ------------- | ----------- |
| name  | string |          |               |             |
| tags  | json   |          |               |             |
| value | string |          |               |             |

返回结果：

```
Status: 200 OK
{
  "headline_id": "",
  "created": "",
}
```

####获取Body列表

```http
GET /apps/<app_id>/body
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |



返回结果：

```
Status: 200 OK
{
    "body": [
        { 
         ...
        },
        ...
    ]
}
```

####获取指定Body

```http
GET /apps/<app_id>/bodys/<body_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |
|      |      |          |               |             |



返回结果：

```
Status: 200 OK
{
    ...
}
```

#### 更新Body

```http
POST /apps/<app_id>/bodys/<body_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签        |

返回结果：

```
Status: 200 OK
```

#### 添加Body

```http
POST /apps/<app_id>/body
```

请求参数：

| Name  | Type   | Required | Default Value | Description |
| ----- | ------ | -------- | ------------- | ----------- |
| name  | string |          |               |             |
| tags  | json   |          |               |             |
| value | string |          |               |             |

返回结果：

```
Status: 200 OK
{
  "body_id": "",
  "created": "",
}
```

####获取CallToAction列表

```http
GET /apps/<app_id>/call_to_action
```

请求参数：

| Name             | Type   | Required | Default Value | Description  |
| ---------------- | ------ | -------- | ------------- | ------------ |
| filter_by_fields | string | no       |               | 筛选字段和值 |
| order_by_fields  | string | no       | 排序规则      |              |
| columns          | string | no       | None          | 列.子列      |
| page             | int    | no       |               |              |
| per_page         | int    | no       |               |              |

返回结果：

```
Status: 200 OK
{
    "call_to_action": [
        { 
         ...
        },
        ...
    ]
}
```

####获取指定CallToAction

```http
GET /apps/<app_id>/call_to_actions/<call_to_action_id>
```

请求参数：

| Name | Type | Required | Default Value | Description |
| ---- | ---- | -------- | ------------- | ----------- |
|      |      |          |               |             |
|      |      |          |               |             |



返回结果：

```
Status: 200 OK
{
    ...
}
```

#### 更新CallToAction

```http
GET /apps/<app_id>/call_to_actions/<call_to_action_id>
```

请求参数：

| Name   | Type   | Required | Default Value | Description |
| ------ | ------ | -------- | ------------- | ----------- |
| name   | string | no       |               | 名称        |
| status | string | no       |               | 状态        |
| tags   | json   | no       |               | 标签        |

返回结果：

```
Status: 200 OK
{
    ...
}
```

#### 添加CallToAction

```http
POST /apps/<app_id>/call_to_action
```

请求参数：

| Name  | Type   | Required | Default Value | Description |
| ----- | ------ | -------- | ------------- | ----------- |
| name  | string | yes      |               |             |
| tags  | json   |          |               |             |
| value | string |          |               |             |

返回结果：

```
Status: 200 OK
{
  "call_to_action_id": "",
  "created": "",
}
```

####ToDo 获取创建实体所需选项的api

