### 账户授权表结构设计

#### `UserOfFacebook`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|facebook_user_id|varchar(50)|主键，fb账号下的user_id|yes|yes|no|
|user_id|interger|cherrypie系统中的user_id|no|yes|no|
|name|varchar(50)|fb中的用户名|no|yes|no|
|email|varchar(50)|fb中绑定的邮箱|no|yes|no|
|token|text|fb用户的token|yes|yes|no|
|status|integer|token的有效状态，1、为有效，2、为无效|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `FacebookUserAccountMap`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|facebook_user_id|varchar(50)|主键|no|yes|no|
|account_id|varchar(50)|主键|no|yes|no|
|status|interger|绑定状态 1、Active 2、Lost|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `UserOfSystem`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|system_user_id|varchar(50)|主键|yes|yes|no|
|manager_id|interger|manager的编号|no|yes|no|
|name|varchar(50)|system user的用户名|no|yes|no|
|role|varchar(50)| EMPLOYEE或者ADMIN，用户的身份|no|yes|no|
|status|interger|system user状态 1、Active 2、Lost|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `SystemUserAccountMap`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|system_user_id|varchar(50)|主键|no|yes|no|
|account_id|varchar(50)|主键|no|yes|no|
|status|interger|绑定状态 1、Active 2、Lost|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `Fanpage`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|page_id|varchar(50)|主键|yes|yes|no|
|name|varchar(50)|主页名称|no|yes|no|
|category|varchar(50)|页面类型|no|yes|no|
|link|varchar(100)|页面网址|no|no|no|
|verification_status|varchar(50)|核实状态|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `ManagerAdAccount` (修改)

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|account_id|varchar(100)|广告账户 id|no|yes|no|
|manager_id|varchar(100)|manager 编号|no|yes|no|
|media|varchar(32)|media|no|yes|no|
|status|integer|广告账户状态：1 为 正常 enable； 2 为 封户 disable 3 为未绑定 unbinding| no|yes|no|
|current_changed_date|datetime|状态改变更新时间|no|yes|no|
|all_changed_date|list dict|状态改变 [{date, (status1, status2)}]|no|yes|no|
|account_name|varchar(100)||no|no|yes|
|last_contract_id|interger||no|no|yes|
|last_contract_name|varchar(100)||no|no|yes|
|extra|json|{"disable_reason": "", "currency": "", "timezone": ""}(新增)|no|no|yes|
|updated|datetime|更新时间|no|no|no|
|created|datetime|创建时间|no|yes|no|

#### `ProductAccountMap`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|product_id|interger|主键|no|yes|no|
|account_id|varchar(50)|主键|no|yes|no|
|status|interger|绑定状态 1、Active 2、Lost|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `ProductPageMap`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|product_id|interger|主键|no|yes|no|
|page_id|varchar(50)|主键|no|yes|no|
|status|interger|page状态 1、默认 2、非默认|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|

#### `FacebookUserPageMap`

| Field | Type | Description | Unique | Index | Null |
| ----- | -----| ------------| ------ | ----- | ---- |
|facebook_user_id|varchar(50)|主键|no|yes|no|
|page_id|varchar(50)|主键|no|yes|no|
|status|interger|page状态 1、默认 2、非默认|no|yes|no|
|created|datetime|创建时间|no|yes|no|
|updated|datetime|更新时间|no|no|no|











