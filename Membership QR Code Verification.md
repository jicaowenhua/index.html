## 会员管理
### 会员二维码获取信息
- **URL**：`/third-api/open/v1/third/user/verifyToken`
- **Method**：`POST`
- **json Body 参数**：
  | 参数     | 必填 | 说明      |
  |------    |------|-----------|
  | token   | 是   | 用户 ID   |
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
```
    --调用 E.g--:
      https://testalb.jicaoge.com/third-api/open/v1/third/user/verifyToken

    --POST data--:
      {
        "token":"eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiI4ZGQ5MWQ0MWQ5OGY0YTc1ODAwMjIwNDRmNzUwMmQ2OCIsInJuZCI6ImNkNDY0NzA2LWY1ZmUtNDk5OC05MjJkLTVkZGVjMGMwOGJiYiIsImV4cCI6MTc1MDE0MzU4NSwiaWF0IjoxNzUwMTQzNTU1fQ.mxXHee8RU3b2NDcYBrRPjWAmTp8a0jajlwlCE1LG3Bw",
        "storeId":82374
      }

    X-Third-Authorization: nonce_str="F56YVzJYn7LMwaczHC6m9VVZ7v3eGPv2",signature="0yNCRU1N5Jb8x5iShrXv1ITa8Sh//9Q/RmaGLfU46oQKjavKPwAomY9atQmFDG8xgIvIOaAZ2WoUSwB5DWNcrD9gp1SGYVklbP3mmgPsiMNolwIofdxLfRDv8KKK9QYCyW4PtyYnXPaNfcpVCLSGt+8oDpe23H2gUsYITu2KJpvcrgD4tg/P+Sl85FBTzFynU9+vJ3gADd77KlA3SoMdXf69CUzGhyAfEF51gvHQ0m8Gbs1+QpQqc8lxzRB20+kRVXkJHLbppzLcu7thME21xaJlF/SeOm7IstqzBYuhEk4unLf5f28yEdnVxDTSq0aZKr73mPAzC/F0Ha+4885qsw==",timestamp="1750124289",serial_no="store001"

```
- **响应成功** (200)：
  ```json
     {
        "traceId":null,
        "code":"200",
        "data":
        {
          "userId":"8dd91d41d98f4a7580022044f7502d68",
          "point":0,
          "expiredSoonPoints":0,
          "balance":2.00
        },
        "errormsg":null,
        "ok":true
    }

- **响应成功** (会员码数据过期)：
  ```json
    {
      "traceId":null,
      "code":"202506161010",
      "data":null,
      "errormsg":"数据过期1",
      "ok":false
    }
- **响应失败** (299 body数据错误)：
  ```json
    {
      "traceId":null,
      "code":"299",
      "data":null,
      "errormsg":"请求失败",
      "ok":false
    }
