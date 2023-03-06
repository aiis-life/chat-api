# AiIsLife 接口文档

### 身份认证

`secret_token` 是代表某个特定用户的永久访问凭证，在访问以下接口时需要附带在 `Authorization` 请求头中，如：

```
Authorization: Bearer <secret_token>
```

目前 `secret_token` 由后台生成，如需使用下面的接口服务，请联系我们

### 创建 session

#### Request

- Method: **POST**
- URL: ```/api/v1/main/session```
- Headers：
    - Content-Type: application/json
    - Authorization: Bearer \<secret_token\>

#### Response

- Body

```json
{
  "code": 0,
  "msg": "success",
  "data": {
    "id": 1,
    "user": "xxx@gmail.com",
    "title": "New chat",
    "created_at": "2023-03-02T12:39:09",
    "updated_at": "2023-03-02T12:39:09"
  }
}
```

### 查询 session 列表

可以通过 id 查询单个 session，这样的话会返回聊天记录（chat_history）

不传任何参数时返回所有 session 列表，不带聊天记录

#### Request

- Method: **GET**
- URL: ```/api/v1/main/session```
- Headers：
    - Content-Type: application/json
    - Authorization: Bearer \<secret_token\>
- QueryParams:
    - id

#### Response

chat_history 聊天记录包含两种角色，role=user/assistant

content 如果聊天结果附带代码块或更加复杂的排版，content 会尽可能使用 Markdown 格式

- Body

```json
{
  "code": 0,
  "msg": "success",
  "data": [
    {
      "id": 1,
      "user": "xxx",
      "title": "你好呀，我们现在开始吧",
      "created_at": "2023-02-15T05:55:01",
      "updated_at": "2023-02-15T05:55:01",
      "chat_history": [
        {
          "role": "user",
          "content": "你好呀，我们现在开始吧"
        },
        {
          "role": "assistant",
          "content": "很高兴能和你一起开始这段旅程！我们可以先谈谈人工智能（AI）吗？"
        }
      ]
    }
  ]
}
```

### 发送聊天消息

#### Request

- Method: **POST**
- URL: ```/api/v1/main/chat```
- Headers：
    - Content-Type: application/json
    - Authorization: Bearer \<secret_token\>
- Body
```json
{
    "session_id": 1,
    "msg": "你好呀，我们现在开始吧"
}
```

#### Response

- Body
```json
{
    "code": 0,
    "msg": "success",
    "data": "很高兴能和你一起开始这段旅程！我们可以先谈谈人工智能（AI）吗？"
}
```
