## 创意库表结构设计

## AssetWarehouse

### `Folder`

| Field         | type      | description                                         | unique  | index     | Null    |
| ------------- | --------- | ----------------------------------------------------| ------- | --------- | ------- |
| folder_id     | integer   | 主键 文件夹 ID                                       | yes     | yes       | no      |
| name   | varchar(50)   | 文件夹名称                                     | no     | yes       | no      |
| email         | varchar(50)   |  用户的 email                                    | no      | yes       | no      |
| default         | integer   |  用来区分是否为默认文件夹                                    | no      | yes       | no      |
| status         | integer   |  用来区分是否已经被删除                                    | no      | yes       | no      |
| created       | datetime  | 创建时间                                            | no      | yes       | no      |
| updated       | datetime  | 更新时间                                            | no      | no        | no      |

### `Asset`

| Field                | type         | description                                  | unique  | index     | Null    |
| ---------------------| ---------    | ---------------------------------------------| ------- | --------- | ------- |
| asset_id          | integer         | 主键                                 | yes     | yes       | no      |
| asset_signature          | varchar(100)         |                              | no     | yes       | no      |
| name        | varchar(50)  |  素材名称                                    | no      | yes       | no      |
| asset_type        | integer  |  素材类型 1:image, 2:video          | no      | yes       | no      |
| width                | 	integer   |  宽度                                        | no      | no       | no      |
| height                | 	integer   |  高度                                        | no      | no       | no      |
| asset_urls         | json |  素材地址及其缩略图地址                                    | no      | no       | yes      |
| creator             | varchar(100)  |  email素材的创建者                                       | no      | yes       | yes      |
| facebook_image_hash             | varchar(100)  |  对应的facebook中的image_hash值                                       | no      | yes       | yes      |
| facebook_video_id             | varchar(50)  |  对应的facebook中的video_id值                                       | no      | yes       | yes      |
| duration             | integer  |  时长单位为 s 用于 video                                       | no      | no       | yes      |
| size                 | integer      |  文件大小                                    | no      | yes       | no      |
| created              | datetime     | 创建时间                                     | no      | yes       | no      |
| updated              | datetime     | 更新时间                                     | no      | no        | no      |

### `FolderAsset`

| Field                | type         | description                                  | unique  | index     | Null    |
| ---------------------| ---------    | ---------------------------------------------| ------- | --------- | ------- |
| folder_asset_id          | integer         | 主键                                 | yes     | yes       | no      |
| asset_id          | integer         | 素材信息 ID                                 | no     | yes       | no      |
| folder_id          | integer         | 文件夹 ID                                 | no     | yes       | no      |
| asset_name        | varchar(50)  |  素材名称                                    | no      | yes       | no      |
| asset_category        | integer  |  素材类型 1: image, 2: video, 3: slideshow     | no      | yes       | no      |
| slideshow_asset | json         |  子素材 ID list 用于 slideshow                     | no      | no       | yes      |
| slideshow_extra | json         |  子素材其他信息 list 用于 slideshow               | no      | no       | yes      |
| inner_audit        | integer  |  内审结果                                    | no      | yes       | yes      |
| outer_audit        | json  |  外审结果                                    | no      | no       | yes      |
| creator          | varchar(50)         | 素材创建者                                 | no     | yes       | no      |
| asset_urls         | json |  素材地址及其缩略图地址                                    | no      | no       | yes      |
| size                 | integer      |  文件大小                                    | no      | yes       | no      |
| status                 | integer      |  素材状态                                    | no      | yes       | no      |
| created              | datetime     | 创建时间                                     | no      | yes       | no      |
| updated              | datetime     | 更新时间                                     | no      | no        | no      |

联合唯一索引：asset_id, folder_id

### `Label`

| Field                | type         | description                                  | unique  | index     | Null    |
| ---------------------| ---------    | ---------------------------------------------| ------- | --------- | ------- |
| label_id          | integer      | 主键 标签 ID                                 | yes     | yes       | no      |
| category          | integer     | 标签类型                                 | no     | yes       | yes      |
| name          | varchar(50)      | 标签名称                                 | no     | yes       | no      |
| created              | datetime     | 创建时间                                     | no      | yes       | no      |
| updated              | datetime     | 更新时间                                     | no      | no        | no      |

### `LabelAsset`

| Field                | type         | description                                  | unique  | index     | Null    |
| ---------------------| ---------    | ---------------------------------------------| ------- | --------- | ------- |
| label_id          | integer      |  主键 标签 ID                               | no     | yes       | no      |
| label_category          | integer     | 标签类别                                 | no     | yes       | yes      |
| asset_id          | integer      | 主键 素材 ID                                 | no     | yes       | no      |
| created              | datetime     | 创建时间                                     | no      | yes       | no      |
| updated              | datetime     | 更新时间                                     | no      | no        | no      |


------


##  广告审核表`Audit`

### `InternalrAudit`  内审是以素材为维度的

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
asset_id|integer|主键|yes|yes|no|
asset_name|string|创意名称|no|yes|no|
asset_type|integer|创意类型 1 image, 2 video, 3 slide|no|yes|no|
linked_ads|integer|关联广告数量|no|no|no|
rejected_ads|integer|外审拒绝广告数量|no|no|no|
status|integer|审核状态 1 未审核 2 通过 3 拒绝|no|no|no|
reason|string|如果状态时拒绝，则审核拒绝原因|no|no|no|
auditor|string|审核人|no|no|no|
category|json|标签类别名称列表 filter用|no|no|no|
label|json|素材的子标签名称列表（filter 用）|no|no|no|
label_detail|json|素材的标签详情（展示 用）|no|no|no|
modified|datetime|创意修改时间|no|no|no|
updated|datetime|内审更新时间|no|no|no|
created|datetime|创建时间|no|no|no|

### `ExternalAudit ` 外审是以广告为维度的，因为从 API 拉取的是广告的状态

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
facebook_ad_id|string|facebook 里的广告 ID, 主键|no|yes|no|
status|string|广告的状态，即我们的外审结果|no|yes|no|
asset_type|integer|创意类型 1 image, 2 video|no|yes|no|
image_hash|string|素材哈希，主键|no|yes|no|
video_id|string|视频 ID, 主键|no|yes|no|
asset_id|varcher(12)|素材 ID|no|yes|no|
media|string|平台|no|yes|no|
account_id|string|广告账户 ID|no|yes|no|
account_status|integer|广告对应的账户状态 活跃 正常 封户|no|yes|no|
creative_detail|json|facebook 中广告创意 ID|no|yes|no|（是否需要存疑）
audit_updated|datetime|拉取审核状态改变的时间，即状态改变时拉取的日期|no|no|no|
facebook_modified|datetime|facebook 中广告的修改时间（包括素材改变或者文案改变）|no|no|no|
text|text|这个广告的 text|no|no|no|
headline|string|这个广告的 headline|no|no|no|
reason|JSON|如果外审状态时拒绝，则拒绝原因|no|no|no|
appeal|integer|如果拒绝，是否已经申诉，1 未申诉 2 已申诉|no|no|no|
auditor|string|操作用户|no|no|no|


