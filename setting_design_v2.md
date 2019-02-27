### API


#### 获取投放平台列表

    GET /settings/[opua|outsouce]_medias

返回结果：

    Status: 200 OK
    {
        "[opua|outsouce]_medias": [
            {
              "media": "",  //投放平台
              "source": ,   //结算方式
            },
            ...
        ]
    }