### API


#### 获取部门列表

    GET /orgs

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no||排序规则|
|page|int|no||
|per_page|int|no||
|columns|string|no|字段筛选|

eg: /v1/orgs?columns=name,company.alias,company.category,creator.name

返回结果：

    Status: 200 OK
    {
        "orgs": [
            { # 参见 OrgInfo
              "org_id": "",
              "superior_org_id": "",
              "category": ,
              "name": "",
              "company_id": xx,
              "company": {
                "alias": "",
                "category": "",
              }
              "offer_effective_date_limit": 1,
              "creator": {
                "name": "xxx",
              },
              "status": 1/2,
              "created": xxx,
              "updated": xxx,
            },
            ...
        ],
        "page": 1,
        "per_page": 1,
        "total": 1,
    }

##### OrgInfo

|Name|Type|Values|Description|
|---|---|---|---|
|org_id|int||部门 ID|
|superior_org_id|int||父级部门 ID|
|category|int||部门类型：1 为 Internal_Advertiser, 2 为 MB_Consulting_Team, 3 为 MB_Agency_Team, 4 为 UA_Department， 5为Finance， 6为Administrator， 7为MediaManagement|
|name|string||部门名称|
|company_id|int||所属公司ID|
|company|dict||所属公司信息对象|
|offer_effective_date_limit|int||offer时间限制配置|
|creator|dict||创建人信息对象|
|status|int||状态：1 为 enabled, 2 为 disabled|
|created|long||创建时间|
|updated|long||更新时间|

#### 创建新的部门

    POST /orgs

请求参数

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|category|int(1..7)|yes||部门类型|
|name|string(100)|no||部门名称|
|superior_org_id|int|no||父级部门ID|
|company_id|int|no||所属公司ID|
|offer_effective_date_limit|int|no|1|是否限制offer的生效时间设置。1为限制，2不限制|


返回结果：

    Status: 200 OK
    {
      "org_id": xx, //新部门的主键
      "created": xxxx //新部门的创建时间
    }

### Model

#### Org

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
org_id|integer|部门 ID, 主键|yes|yes|no|
super_org_id|integer|父级部门 ID|yes|yes|yes|
category|integer|部门分类：1 为 Internal Advertiser，2 为 MB Consulting Team，3 为 MB Agency Team，4 为 UA Department，5 为 Finance, 6 为 Administrator, 7为MediaManagement|no|yes|no|
name|varchar(100)|部门名称|yes|yes|no|
company_id|integer|公司 ID|no|yes|yes|
status|integer|状态：1 为 enabled,2 为 disabled|no|yes|no|
offer_effective_date_limit|integer||no|yes|no|
creator|integer||no|no|yes|
updated|datetime|更新时间|no|yes|no|
created|datetime|创建时间|no|yes|no|

联合唯一索引：category, name