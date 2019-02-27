### API

#### 创建 Region 组

    POST /orgs/<org_id>/region_groups

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|name|string|yes||组名称|
|regions|list string|yes||列表|

返回结果：

    Status: 200 OK
    {
      "region_group_id": "",
      "created": ""
    }

#### 获取 Region 组列表

    GET /orgs/<org_id>/region_groups

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no|筛选|
|order_by|string|no|排序规则|
|page|int|no||
|per_page|int|no||

返回结果：

    Status: 200 OK
    {
      "region_groups": [
      {
    	"region_group_id": "",
    	"name": "",
    	"regions": [],
    	"created": ""
      },
      ...
      ]
    }
#### 删除 RegionGroup 列表

    DELETE 	/orgs/<org_id>/region_groups/<region_group_id>

返回结果：
​    Status: 200 OK

### Model

#### RegionGroup

| field    | type         | description | unique | index | NULL |      |
| -------- | ------------ | ----------- | ------ | ----- | ---- | ---- |
| group_id | integer      | 主键        | yes    | yes   | no   |      |
| org_id   | integer      | 组织 ID     | no     | yes   | no   |      |
| name     | varchar(300) | 组织名称    | yes    | yes   | no   |      |
| regions  | list string  | 列表        | no     | no    | no   |      |
| updated  | datetime     | 更新时间    | no     | yes   | no   |      |
| created  | datetime     | 创建时间    | no     | yes   | no   |      |

### 