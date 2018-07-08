# CNJS后端[API文档](http://apidoc.asmodeus.cn/web/#/1)
## [在线文档](http://apidoc.asmodeus.cn/web/#/1)采用showdoc搭建
如何部署showdoc在线文档，请参考[这里](./apidoc/README.md)
# 静态API文档
### GET /topics 主题首页
    
**简要描述：** 

- 获得主题首页内容

**请求URL：** 
- ` http://cnjs.asmodeus.com/api/v1/topics `
  
**请求方式：**
- GET 

**参数：** 

|参数名|类型|说明|
|:----   |:----- |-----   |
|page  |number |页数   |
|tab |string |主题分类。目前有 ask share job good|
|limit  |number | 每一页的主题数量    |
|mdrender  |string | 当为 false 时，不渲染。默认为 true，渲染出现的所有 markdown 格式文本。   |

 **返回示例**



 ``` 
 { 
     "success" : "true", 
     "data" : { 
          "0" : { 
               "id" : "5a9661ff71327bb413bbff5b", 
               "author_id" : "5110f2bedf9e9fcc584e4677", 
               "tab" : "share", 
               "content" : "HTML code", 
               "title" : "求支持", 
               "last_reply_at" : "2018-06-22T06:21:44.773Z", 
               "good" : "true", 
               "top" : "true", 
               "reply_count" : 38, 
               "visit_count" : 6257, 
               "create_at" : "2018-06-14T09:57:49.652Z", 
               "author" : { 
                    "loginname" : "admin", 
                    "avatar_url" : "https://avatars3.githubusercontent.com/u/2842176?v=4&s=120" 
               } 
          }, 
          "2" : { 
               "id" : "54bb8bb869ceba1d387bbfad", 
               "author_id" : "541bf946ad60405c1f14b770", 
               "tab" : "ask", 
               "content" : "HTML Code", 
               "title" : "测试", 
               "last_reply_at" : "2018-06-04T17:43:04.345Z", 
               "good" : "false", 
               "top" : "false", 
               "reply_count" : 19, 
               "visit_count" : 10956, 
               "create_at" : "2018-05-18T10:32:24.177Z", 
               "author" : { 
                    "loginname" : "test", 
                    "avatar_url" : "https://avatars0.githubusercontent.com/u/3739368?v=4&s=120" 
               } 
          }, 
		  ...
	}
}
```

 **返回数据参数说明** 
- success 返回成功标志，string类型

| 值 | 描述 |
|:---- |-----   |
| true | 成功返回数据 |
| false | 提交数据错误 |

-  data 类型：对象数组，代表各个主题的概要信息

| 参数 | 类型 | 描述 |
|:----   |:----- |-----   |
| id | string| 主题ID编号 |
| author_id | string| 作者ID编号 |
| tab | string| 所属分类 |
| content | string| 内容，如果请求参数`mdrender`为`true`，即返回已经渲染过的HTML格式内容，否则为markdown格式内容 |
| title | string| 主题的标题 |
| last_reply_at | date | 最后回复时间 |
| good | string| `true`加精；`false`未加精 |
| top | string| `true`置顶；`false`未置顶 |
| reply_count | number| 回复数 |
| visit_count | number| 浏览数 |
| create_at | date | 创建时间 |
| - - author |object  | 包含两个子属性：`loginname`，string，作者登录名；`avatar_url`，string，头像的URL |



 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### GET /topic/:id 主题详情
    
**简要描述：** 

- 获得指定id主题的详细内容

**请求URL：** 
- ` http://cnjs.asmodeus.com/api/v1/topics/:id `
  
**请求方式：**
- GET 

**参数：** 

|参数名|类型|说明|
|:----   |:----- |-----   |
|mdrender  |string | 当为 false 时，不渲染。默认为 true，渲染出现的所有 markdown 格式文本。   |
|accesstoken |string |用户的token。当需要知道一个主题是否被特定用户收藏以及对应评论是否被特定用户点赞时，才需要带此参数。会影响返回值中的 `is_collect` 以及 replies 列表中的 `is_uped` 值。|

 **返回示例**

```
 {
    "success":"true", 
    "data": {
         "id":"5433d5e4e737cbe96dcef312", 
         "author_id":"504c28a2e2b845157708cb61", 
         "tab":"share", 
         "content":"HTML code", 
         "title":"test", 
         "last_reply_at":"2018-07-01T06:52:51.580Z", 
         "good":"true", 
         "top":"false", 
         "reply_count":92, 
         "visit_count":37863, 
         "create_at":"2018-06-07T12:00:36.270Z", 
         "author": {
              "loginname":"alsotang", 
              "avatar_url": "https://avatars1.githubusercontent.com/u/1147375?v=4&s=120" 
         }, 
         "replies":[
              "0": {
                   "id":"5433d866e737cbe96dcef313", 
                   "author": {
                        "loginname":"leapon", 
                        "avatar_url": "https://avatars1.githubusercontent.com/u/4295945?v=3&s=120" 
                   }, 
                   "content":"HTML code", 
                   "ups": {
                        "0":"5404a4120256839f712590f3", 
                        "1":"50f3b267df9e9fcc58452224", 
						...,
                   }, 
                   "create_at":"2014-10-07T12:11:18.981Z", 
                   "reply_id": "", 
                   "is_uped":"false"
              }, 
              "1": {},
			  ...,
	     ]
         "is_collect":"false"
    }
}
```

 **返回数据参数说明** 
- success 返回成功标志，string类型

| 值 | 描述 |
|:---- |-----   |
| true | 成功返回数据 |
| false | 提交数据错误 |

-  data 类型：对象，代表各个主题的概要信息

|参数|类型|描述|
|:-------|:-------|:-------|
| id | string| 主题id |
| author_id | string| 作者id |
| tab | string| 分类 |
| content | string| 内容，如果请求参数`mdrender`为`true`，即返回已经渲染过的HTML格式内容，否则为markdown格式内容 |
| title | string| 主题的标题 |
| last_reply_at | date | 最后回复时间 |
| good | string| `true`加精；`false`未加精 |
| top | string| `true`置顶；`false`未置顶 |
| reply_count | number| 回复数 |
| visit_count | number| 浏览数 |
| create_at | date | 创建时间 |
| author |object  | 包含两个子属性：`loginname`，string，作者登录名；`avatar_url`，string，头像的URL |
| replies |object  | 所有回复，具体结构详见后面 |
| is_collect | string| 如果请求参数`acesstoken`有提交，则返回该主题是否被对应token用户收藏。`true`已收藏；`false`未收藏  |

-  replies 类型：对象数组，该主题所有的回复。
如果有回复，从第一条回复开始，对应属性名（数组下标）`0`、`1`、`2`...以此类推。每条回复对象的具体内容如下。

|参数|类型|描述|
|:-------|:-------|:-------|
| id | string| 回复id |
| author |object  | 包含两个子属性：`loginname`，string，作者登录名；`avatar_url`，string，头像的URL |
| content | string| 内容，如果请求参数`mdrender`为`true`，即返回已经渲染过的HTML格式内容，否则为markdown格式内容 |
| ups |object  | 点赞用户。属性名从`0`、`1`、`2`开始以此类推，代表每个点赞用户，内容是用户的id|
| create_at | date | 创建时间 |
| reply_id |string  | 如果不为空，则代表replies对象所回复内容的回复id |
| is_uped | string| 如果请求参数`acesstoken`有提交，则返回该回复是否被对应token用户点赞。`true`已点赞；`false`未点赞 |


 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### POST /topics 新建主题
    
**简要描述：** 

- 创建一个新的主题

**请求URL：** 
- ` http://cnjs.asmodeus.com/api/v1/topics `
  
**请求方式：**
- POST 

**参数：** 

|参数名|类型|说明|
|:----   |:----- |-----   |
|accesstoken   |string |用户的 `accessToken`   |
|title  |string | 主题的标题    |
|tab |string |主题分类。目前有 ask share job good|
|content |string |主题的内容|

 **返回示例**



 ``` 
{
     "success" : "true", 
     "topic_id": "6633d42ee737cbe962e2a2"
}
```

 **返回数据参数说明** 


| 参数 | 类型 | 描述 |
|:----   |:----- |-----   |
| success | string | 返回成功标志。`true`:成功返回数据； `false`：提交数据错误|
| topic_id | string| 所创建主题的对应的id |



 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### POST /topics 编辑主题
    
**简要描述：** 

- 编辑指定id的主题

**请求URL：** 
- ` http://cnjs.asmodeus.com/api/v1/topics/update `
  
**请求方式：**
- POST 

**参数：** 

|参数名|类型|说明|
|:----   |:----- |-----   |
|topic_id  |string | 想要编辑的主题的id    |
|accesstoken   |string |用户的 `accessToken`   |
|title  |string | 主题的标题    |
|tab |string |主题分类。目前有 ask share job good|
|content |string |主题的内容|

 **返回示例**



 ``` 
{
     "success" : "true", 
     "topic_id": "6633d42ee737cbe962e2a2"
}
```

 **返回数据参数说明** 


| 参数 | 类型 | 描述 |
|:----   |:----- |-----   |
| success | string | 返回成功标志。`true`:成功返回数据； `false`：提交数据错误或无权编辑该主题|
| topic_id | string| 所创建主题的对应的id |



 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### POST /topic_collect/collect 收藏主题
    
**简要描述：** 

- 收藏某一主题页


**请求方式：**
- POST

**参数：** 

|参数名|类型|说明|
|:----   |:----- |-----   |
|accesstoken  |string |用户的 accessToken   |
|topic_id |string |主题的id|

 **返回值示例**



 ``` 
 {"success": true}

```

 **返回数据参数说明** 
- success 返回成功标志，string类型

| 值 | 描述 |
|:---- |-----   |
| true | 成功返回数据 |
| false | 提交数据错误 |

 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### POST /topic_collect/de_collect 取消主题
    
**简要描述：** 

- 取消收藏某一主题页


  
**请求方式：**
- POST

**参数：** 

|参数名|类型|说明|
|:----   |:----- |-----   |
|accesstoken  |string |用户的 accessToken   |
|topic_id |string |主题的id|

 **返回值示例**



 ``` 
 {"success": true}

```

 **返回数据参数说明** 
- success 返回成功标志，string类型

| 值 | 描述 |
|:---- |-----   |
| true | 成功返回数据 |
| false | 提交数据错误 |

 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### GET /topic_collect/:loginname 用户所收藏的主题
    
**简要描述：** 

- 获取用户所收藏的所有主题页

**请求URL：** 
-  http://cnjs.asmodeus.com/api/v1/topic_collect/alsotang
  
**请求方式：**
- GET


 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### POST /topic/:topic_id/replies 新建评论
    
**简要描述：** 

- 新建一条评论


**请求方式：**
- POST

**参数：** 

|参数名|类型|说明|
|:----   |:----- |-----   |
|accesstoken  |string |用户的 accessToken   |
|reply_id |string |如果这个评论是对另一个评论的回复，请务必带上此字段。这样前端就可以构建出评论线索图。|
|content  |string |评论的主体  |

 **返回示例**

 ``` 
{
     "success" : "true", 
     reply_id: '5433d5e4e737cbe96dcef312'
}
```

 **返回数据参数说明** 


| 参数 | 类型 | 描述 |
|:----   |:----- |-----   |
| success | string | 返回成功标志。`true`:成功返回数据； `false`：提交数据错误或无权编辑该主题|
| reply_id | string| 所新建评论对应的id|


 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### POST /reply/:reply_id/ups 为评论点赞
    
**简要描述：** 

- 为某条评论点赞


**请求方式：**
- POST

**参数：** 

|参数名|类型|说明|
|:----   |:----- |-----   |
|accesstoken  |string |接口会自动判断用户是否已点赞，如果否，则点赞；如果是，则取消点赞。点赞的动作反应在返回数据的 `action` 字段中，`up` or `down`   |

 **返回示例**

 ``` 
{
     "success": true, 
	 "action": "down"
}
```

 **返回数据参数说明** 


| 参数 | 类型 | 描述 |
|:----   |:----- |-----   |
| success | string | 返回成功标志。`true`:成功返回数据； `false`：提交数据错误或无权编辑该主题|
| action | string| 返回点赞或取消点赞。`up`：点赞成功；`down`：取消点赞成功|


 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### GET /user/:loginname 用户详情
    
**简要描述：** 

- 获取用户详情页面

**请求URL：** 
- ` http://cnjs.asmodeus.com/api/v1/user/alsotang `

**请求方式：**
- GET


 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### POST /accesstoken 验证 accessToken 的正确性
    
**简要描述：** 

- 验证 accessToken 的正确性


**请求方式：**
- POST

**参数：** 

|参数名|类型|说明|
|:----   |:----- |-----   |
|accesstoken  |string |用户的 accessToken。如果成功匹配上用户，返回成功信息。否则 403。   |

 **返回示例**

 ``` 
{
     success: true, 
	 loginname: req.user.loginname, 
	 id: req.user.id, 
	 avatar_url: req.user.avatar_url
}
```

 

 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### GET /message/count 获取未读消息数
    
**简要描述：** 

- 获取未读消息数


  
**请求方式：**
- GET 

**参数：** 

|参数名|类型|
|:----   |:----- |
|accesstoken |string |



 **返回值示例**



 ``` 
 {  data: 3 }
```


 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### GET /messages 获取已读和未读消息
    
**简要描述：** 

- 获取所有的已读消息和未读消息

**请求URL：** 
- ` http://cnjs.asmodeus.com/api/v1/topics `
  
**请求方式：**
- GET 

**参数：** 

|参数名|类型|说明|
|:----   |:----- |-----   |
|accesstoken  |string |页数   |
|mdrender  |string | 当为 `false` 时，不渲染。默认为 `true`，渲染出现的所有 markdown 格式文本。   |

 **返回值示例**



 ``` 
 { 
     data: {
    has_read_messages: [],
    hasnot_read_messages: [
      {
        id: "543fb7abae523bbc80412b26",
        type: "at",
        has_read: false,
        author: {
          loginname: "alsotang",
          avatar_url: "https://avatars.githubusercontent.com/u/1147375?v=2"
        },
        topic: {
          id: "542d6ecb9ecb3db94b2b3d0f",
          title: "adfadfadfasdf",
          last_reply_at: "2014-10-18T07:47:22.563Z"
        },
        reply: {
          id: "543fb7abae523bbc80412b24",
          content: "[@alsotang](/user/alsotang) 哈哈",
          ups: [ ],
          create_at: "2014-10-16T12:18:51.566Z"
          }
        },
    ...
    ]
  }
}
```





 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### POST /message/mark_all 标记全部已读
    
**简要描述：** 

- 获得主题首页内容

**请求方式：**
- POST 

**参数：** 

|参数名|类型|
|:----   |:----- |
|accesstoken |string |


 **返回值示例**



 ``` 
 { 
    success: true,
    marked_msgs: [ { id: '544ce385aeaeb5931556c6f9' } ] 
}
```

 **返回数据参数说明** 
- success 返回成功标志，string类型

| 值 | 描述 |
|:---- |-----   |
| true | 成功返回数据 |
| false | 提交数据错误 |




 **备注** 

- 更多返回错误代码请看首页的错误代码描述

### POST /message/mark_one/:msg_id 标记单个消息为已读
    
**简要描述：** 

- 标记单个消息为已读

**请求URL：** 
- ` http://cnjs.asmodeus.com/api/v1//message/mark_one/58ec7d39da8344a81eee0c14`
  
**请求方式：**
- POST

**参数：** 

|参数名|类型|
|:----   |:----- |
|accesstoken  |string |

 **返回值示例**

 ``` 
 { 
     success: true,
     marked_msg_id: "58ec7d39da8344a81eee0c14"
}
```

 **返回数据参数说明** 
- success 返回成功标志，string类型

| 值 | 描述 |
|:---- |-----   |
| true | 成功返回数据 |
| false | 提交数据错误 |



 **备注** 

- 更多返回错误代码请看首页的错误代码描述

