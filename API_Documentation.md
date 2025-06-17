# API 文档

## 会员管理

### 会员余额
- **URL**：`/third-api/open/v1/third/userBalance`
- **Method**：`POST`
- **json Body 参数**：
  | 参数     | 必填 | 说明      |
  |------    |------|-----------|
  | userId   | 是   | 用户 ID   |
  | storeId   | 是   |  store_code  |
- **请求头**：
   - **name**：`X-Third-Authorization`
  - **请求头构建 参数**：
    | 参数     | 必填 | 说明      |
    |------    |------|-----------|
    | nonce_str   | 是   | 32位随机随机数 E.g:"F56YVzJYn7LMwaczHC6m9VVZ7v3eGPv2" |
    | signature   | 是   |  Base64编码签名结果  |
    | timestamp   | 是   |  秒级时间戳 E.g:1750124289 |
    | serial_no   | 是   |  store001  (固定值)  |

- **响应成功** (200)：
  ```json
  {
    "traceId":null,
    "code":"200",
    "data":
    {
        "storeId":"82374",
        "userId":"8dd91d41d98f4a7580022044f7502d68",
        "balance":2.00
    },
    "errormsg":null,
    "ok":true
  }
- **响应失败** (401 证书校验失败)：
  - HTTP/1.1 401 Unauthorized
- **响应失败** (404 URL错误 or 参数错误)：
  ```json
    {
      "timestamp":"2025-06-16T10:34:54.600+00:00",
      "path":"/open/v1/third/userBalance",
      "status":404,
      "error":"Not Found",
      "message":null,
      "requestId":"f5816e9c-978657"
    }
