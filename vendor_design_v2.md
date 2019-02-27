### API

#### 获取 vendor_account (account_setting) 列表

    GET /orgs/<org_id>/companies/<company_id>/vendor_account

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|filter_by|string|no||筛选|
|order_by|string|no|排序规则|
|distinct_by|string|no||
|page|int|no||
|per_page|int|no||

返回结果：

    Status: 200 OK
    {
        "vendor_account": [
            {
              "payee": "",
              "media": ,
              "account_id": "",
            },
            ...
        ]
    }


#### 新增 vendor_account(account_setting) 列表

    POST /orgs/<org_id>/companies/<company_id>/vendor_account

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|vendor_account|list VendorAccount(dict)|no||vendor 账户|

##### VendorAccount

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|media|string|yes|||
|account_id|string|yes|||


返回结果：

    Status: 200 OK

#### 修改 单个 vendor_account(account_setting)

    PUT /orgs/<org_id>/companies/<company_id>/vendor_account/<media_account_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|account_id|string|yes|---|---|
|media|-string|yes|---|---|


返回结果：

    Status: 200 OK

#### 删除 单个 vendor_account(account_setting) 列表

    DELETE /orgs/<org_id>/companies/<company_id>/vendor_account/<media_account_id>

请求参数：

无

返回结果：

    Status: 200 OK
