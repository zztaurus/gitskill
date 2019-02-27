创意库 api 设计方案

### AssetWarehouse

#### 获取素材列表

        GET /creative/assets

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| page  | integer  | no       | 1             | 页号        |
| per_page  | integer  | no       | 10             | 每页条数        |
| order_by  | string  | no       | 无             | 排序规则        |
| filter_by | string  | no       | 无             | 筛选          |


返回结果：

    Status: 200 OK
    {
    	'assets': [
    		{
    			'folder_asset_id':'',
    			'folder_id':'',
    			'asset_name':'',
    			'asset_category':'',
    			'creator':'',
    			'inner_audit':'',
    			'inner_reject_reason':'',
    			'outer_audit':{"passed_num": "", "rejected_num": ""}, 
    			'updated':'',
    			'created':'',
          },
       		...
       ]
       'total': '',
       'page': '',
       'per_page': ''
    }

#### 获取素材详情

        GET /creative/assets/<folder_asset_id>

返回结果：

    Status: 200 OK
    {
    	'folder_asset_id':'',
    	'folder_id':'',
    	'asset_name':'',
    	'asset_category':'',
    	'asset_labels':[
    		{
    			'category': '',
    			'category_name': '',
    			'labels': [
    				{'label_id': '', 'label_name': ''},
    			]
    		},
    	]
    	'slideshow_data':{
    		"extra": {},
    		"data": [
    		{
    		'width':'',
    		'height':'',
    		'asset_urls':{},
    			}
    		]
    		},
    	'image_data':{
    		"data": {
    
    		'width':'',
    		'height':'',
    		'asset_urls':{},
    		},
    	'video_data':{
    		"data": {
    
    		'asset_urls':{},
    		'duration':'',}
    		},
    	'inner_audit':'',
    	'size':'',
    	'creator':'',
    	'updated':'',
    	'created':'',
    	'campaign_num': '',
    	'adset_num':'',
    	'ad_num': ''
     }


#### 新增 image/video 素材

        POST /creative/assets

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| folder_id | integer  | yes       | 无             | 文件夹 ID        |
| category | integer  | yes       | 无             | 素材类型  1:image, 2:video, 3:slideshow      |
| assets | json  | yes       | 无             | 素材 asset [{"asset_id": "", "name": ""}, {}]     |
| asset_labels | json  | no       | 无             | 素材标签 [{category: "", label_ids: []}, {}]       |

返回结果：

    Status: 200 OK

#### 新增 slideshow 素材

        POST /creative/assets/slideshow

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| folder_id | integer  | yes       | 无             | 文件夹 ID        |
| slideshow_asset | json  | no       | 无             | 素材为 slideshow 的子素材的 id 列表      |
| slideshow_extra | json  | no       | 无             | 素材为 slideshow 的额外信息{"ratio": "", "interval": "", "effect": ""}      |
| asset_name | string  | yes       | 无             | 素材名称        |
| asset_labels | json  | no       | 无             | 素材标签 [{category: "", label_ids: []}, {}]       |

返回结果：

    Status: 200 OK

#### 修改素材

        PUT /creative/assets/<folder_asset_id>

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| asset_name | string  | no       | 无             | 素材名称        |
| asset_labels | json  | no       | 无             | 素材标签 [{category: "", label_ids: []}, {}]       |

返回结果：

    Status: 200 OK

#### 删除素材

        PUT /creative/assets/<folder_asset_id>/disabled

返回结果：

    Status: 200 OK


#### 复制素材

        POST /creative/assets/<folder_asset_id>/copy

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| folder_id | string  | yes       | 无             | 新的文件夹 ID        |

返回结果：

    Status: 200 OK

#### 移动素材

        PUT /creative/assets/<folder_asset_id>/move

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| folder_id | string  | yes       | 无             | 新的文件夹 ID        |

返回结果：

    Status: 200 OK

#### 批量移动素材

        PUT /creative/assets/move

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| folder_id | string  | yes      | 无             | 新的文件夹 ID        |
| folder_asset_ids | json  | yes      | 无             |素材id列表        |

返回结果：

    Status: 200 OK

#### 分享素材

        POST /creative/assets/<folder_asset_id>/share

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| email | string  | yes       | 无             |  被分享人的邮箱       |

返回结果：

    Status: 200 OK

#### 上传图片素材

	POST /creative/assets/images

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|file|File|no||文件流|
|url|str|no||第三方文件链接|
|file_name|str|no||自定义文件名|


返回结果：

    Status: 200 OK
    {
      "file_name": "",
      "asset_urls": {"origin: ""http://xxxx", "48w": "", "128w": ""},
      "asset_id": ""
    }

#### 上传视频素材

	POST /creative/assets/videos

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|file|File|no||文件流|
|url|str|no||第三方文件链接|
|file_name|str|no||自定义文件名|


返回结果：

    Status: 200 OK
    {
      "file_name": "",
      "asset_urls": {"origin: ""http://xxxx", "48w": "", "128w": ""},
      "asset_id": ""
    }

#### 获取标签类别列表

        GET /creative/assets/categories

返回结果：

    Status: 200 OK
    {
    	'categories': [
    		{
    			'category':'',
    			'name':'',
    			'updated':'',
    			'created':'',
          },
       		...
       ]
    }

#### 新增标签类别

        POST /creative/assets/categories

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| name | string  | yes       | 无             | 标签类别名称        |

返回结果：

    Status: 200 OK

#### 获取标签列表

        GET /creative/assets/categories/<category>/labels

返回结果：

    Status: 200 OK
    {
    	'labels': [
    		{
    			'label_id':'',
    			'category':'',
    			'name':'',
    			'updated':'',
    			'created':'',
          },
       		...
       ]
    }


#### 通过类别名称获取标签列名称表

        GET /creative/assets/category/label_name

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| category_name | string  | yes       | 无             | 标签类别名称        |

返回结果：

    Status: 200 OK
    {
    	'labels': [name1, name2, ... ]
    }
#### 新增标签

        POST /creative/assets/categories/<category>/labels

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| name | string  | yes       | 无             | 标签名称        |

返回结果：

    Status: 200 OK

#### 获取 文件夹 列表

        GET /creative/folders

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| page  | integer  | no       | 1             | 页号        |
| per_page  | integer  | no       | 10             | 每页条数        |
| order_by  | string  | no       | 无             | 排序规则        |
| filter_by | string  | no       | 无             | 筛选          |


返回结果：

    Status: 200 OK
    {
    	'folders': [
    		{
    			'folder_id':'',
    			'name':'',
    			'default':'',
    			'email':'',
    			'asset_num':'',
    			'updated':'',
    			'created':'',
          },
       		...
       ]
       'total': '',
       'page': '',
       'per_page': ''
    }

#### 新建 文件夹

        POST /creative/folders

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| name  | string  | yes       | 无             | 文件夹名称        |

返回结果：

    Status: 200 OK
    {
    	'folder_id': '',
    	'created': ''
    	}


#### 修改 文件夹

        PUT /creative/folders/<folder_id>

 请求参数：

| Name      | Type    | Required | Default Value | Description |
| --------- | ------- | -------- | ------------- | ----------- |
| name  | string  | yes       | 无             | 文件夹名称        |

返回结果：

    Status: 200 OK

#### 删除 文件夹

        PUT /creative/folders/<folder_id>/disabled

返回结果：

    Status: 200 OK

------

`Ad Review API`

#### 获取素材内部审核列表

    GET /creative/internal_audit

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer |no|1|页码|
|per_page|integer |no|10|每页的条数|
|order_by|string |no|无|排序规则|
|filter_by|string |no|无|筛选规则|


返回结果：

    Status: 200 OK
    {
        "internal_audits": [
            { # 参见 InternalAudit
    			'folder_asset_id': {
    				# 见 FolderAsset
    				...
    			},
    			'asset_name': '',
                'connected_ads': '',
                'rejected_ads': '',
                'status': '',
                'reason': '',
                'auditor': '',
    			'rask': '',
                'label': '',
    			'modified': '',
    			'updated': '',
    			'created': '',
            },
            ...
        ]
    }


#### 由内审素材获得外审广告信息

    GET /creative/internal_audit/<folder_asset_id>/external_audit

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer |no|1|页码|
|per_page|integer |no|10|每页的条数|
|order_by|string |no|无|排序规则|
|filter_by|string |no|无|筛选规则|

返回结果：

    Status: 200 OK
    {
        "external_audits": [
            { # 参见 ExternalAudit
              'facebook_ad_id':'',
              'media':'',
              'account_id':'',
              'account_status':'',
              'creative_id':'',（待榷）
              'audit_updated':'',
              'facebook_modified':'',
              'status':'',
              'reason':'',
              'appeal':'',
              'auditor':'',
            },
            ...
        ]
    }


#### 获取外审列表信息

    GET /creative/external_audit

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer |no|1|页码|
|per_page|integer |no|10|每页的条数|
|order_by|string |no|无|排序规则|
|filter_by|string |no|无|筛选规则|

返回结果：

    Status: 200 OK
    {
        "external_audits": [
            { # 参见 ExternalAudit
              'facebook_ad_id':'',
              'asset_id':'',
    		  'asset_info':{
    			  # 参见 Asset
    		  }
              'media':'',
              'account_id':'',
              'account_status':'',
              'creative_id':'',（待榷）
              'audit_updated':'',
              'facebook_modified':'',
              'status':'',
              'reason':'',
              'appeal':'',
              'auditor':'',
            },
            ...
        ]
    }


#### 广告内审 （外审全部由 API 拉取，无接口）

    PUT /creative/internal_audit/<operation>
    
    operation 的值有 1. passed 2. rejected

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|folder_asset_ids|array(int) |||要进行内审的 ID 的列表|
|reason| string|||审核未拒绝时需要，拒绝的原因|

返回结果：

    Status: 200 OK

#### 内审广告风险标注

    PUT /creative/internal_audit/<folder_asset_id>/risk

返回结果：

    Status: 200 OK


#### 广告申诉

    PUT /creative/external_audit/<facebook_ad_id>/appeal

返回结果：

    Status: 200 OK


`Top Asset API`

### 获取创意排行榜列表

    GET /creative/top_assets/roles/<role_id>

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|page|integer |no|1|页码|
|per_page|integer |no|10|每页的条数|
|order_by|string |no|无|排序规则|
|filter_by|string |no|无|筛选规则|
|group_by|string |no|无|分组规则|
|save_csv|bool |no|无|是否保存 CSV|
|view_id|integer |no|20|要查询的view id|

返回结果：

    Status: 200 OK
    {
        "top_assets": [
            { # 参见 TopAsset
              'asset_id':'',
              'name':'',
              'impressions':'',
              'clicks':'',
              'installs':'',
              'ctr':'',
              'install_rate':'',
              'rr':'',
              'designer':'',
            },
            ...
        ]
    }


### 获取创意排行榜中某个素材的详细

    GET /creative/top_assets/<asset_id>

返回结果：

    Status: 200 OK
    {   # 参见 Asset
        'asset_id':'',
        'name':'',
        'category':'',
        'sub_asset':'',
        'sub_asset_id':[],
        'width':'',
        'height':'',
        'asset_url':'',
        'thumbnail_url':'',
        'duration':'',
        'size':'',
        'created':'',
        'updated': ''
     }

### 收藏此创意

    POST /creative/top_assets/<asset_id>/collect

返回结果：

    Status: 200 OK









