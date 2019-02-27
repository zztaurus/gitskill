### API

#### 登出
	POST /oauth2/logout
	
#### 通过Google登陆
	GET /oauth2/gmail_oauth2

请求参数：

|Name|Type|Required|Default Value|Description|
|---|---|---|---|---|
|email|string |yes||google email|


### Model

#### ClientOfOauth2

field|type|description|unique|index|NULL|
---|---|---|---|---|---|---|---|---|---|---|
client_id|varchar(32)|主键|yes|yes|no|
client_secret|varchar(100)||no|yes|no|
name|varchar(100)||no|yes|no|
updated|datetime||no|yes|no|
created|datetime||no|yes|no|
