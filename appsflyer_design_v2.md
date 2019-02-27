
#### 获取 media_config 列表

    GET /orgs/<org_id>/companies/<company_id>/media_config

请求参数：

无

返回结果：

    Status: 200 OK
    {
        "media_config": [
            {
              "payee": "",
              "media": ,
              "media_source": "",
            },
            ...
        ]
    }

#### 修改与新建 media_config 列表

    PUT /orgs/<org_id>/companies/<company_id>/media_config

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|media_config|list MediaConfig|yes||media 的配置|


#### 获取Vendor的appsflyer配置信息列表

    GET /companies/<company_id>/appsflyer_infos

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no|排序规则|
|page|int|no||
|per_page|int|no||

返回结果：

    Status: 200 OK
    {
        "appsflyer_infos": [
            {
              "agency_type": "",
              "media": ,
              "agency": ,
              "payee": "",
              "media_source": "",
              "updated": "",
              "created": "",
            },
            ...
        ]
    }