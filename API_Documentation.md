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
```
    --调用 E.g--:
      https://testalb.jicaoge.com/third-api/open/v1/third/userBalance

    --POST data--:
      {
        "userId":"8dd91d41d98f4a7580022044f7502d68",
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


### 会员余额支付
- **URL**：`/third-api/open/v1/third/payBalance`
- **Method**：`POST`
- **json Body 参数**：
  | 参数     | 必填 | 说明      |
  |------    |------|-----------|
  | userId   | 是   | 用户 ID   |
  | storeId   | 是   |  store_code  |
  | amount   | 是   |  商品金额    |
  | orderSn   | 是   |  订单号  |
  | operateId   | 是   |  操作id  |
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
      https://testalb.jicaoge.com/third-api/open/v1/third/payBalance

    --POST data--:
      {
        "userId":"8dd91d41d98f4a7580022044f7502d68",
        "storeId":82374,
        "amount":1,
        "orderSn":"NG202506171000117904473395842575",
        "operateId":"order_create_20230821001"
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
      "transId":1,
      "transNo":"20250617112735522033413544306818",
      "userCardId":62,
      "operationType":"consume",
      "amount":1,
      "balanceType":"cash",
      "beforeBalance":2.00,
      "cashAmount":1.00,
      "couponAmount":0.00,
      "afterBalance":1.00,
      "storeId":2,
      "referenceId":"NG202506171000117904473395842575",
      "operatorId":"order_create_20230821001",
      "transTime":"2025-06-17T11:27:35.522922015",
      "refundTransId":null,
      "remark":"{\"balance\":2.00,\"cardId\":62,\"cashBalance\":1.00,\"couponBalance\":1.00,\"createTime\":\"2025-06-16 20:48:36\",\"updateTime\":\"2025-06-16 20:48:36.745\",\"userCardId\":62,\"userId\":\"8dd91d41d98f4a7580022044f7502d68\",\"version\":0}"
     },
    "errormsg":null,
    "ok":true
    }


### 会员售后退款
- **URL**：`/third-api/open/v1/third/refund`
- **Method**：`POST`
- **json Body 参数**：
  | 参数     | 必填 | 说明      |
  |------    |------|-----------|
  | userId   | 是   | 用户 ID   |
  | storeId   | 是   |  store_code  |
  | amount   | 是   |  商品金额    |
  | orderSn   | 是   |  订单号  |
  | operateId   | 是   |  操作id  |
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
      https://testalb.jicaoge.com/third-api/open/v1/third/refund

    --POST data--:
      {
        "userId":"8dd91d41d98f4a7580022044f7502d68",
        "storeId":82374,
        "amount":1,
        "orderSn":"NG202506171000117904473395842575",
        "operateId":"order_create_20230821001"
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
        "transId":3,
        "transNo":"20250617134330577150439612442423",
        "userCardId":62,
        "operationType":"consume",
        "amount":1,
        "balanceType":"cash",
        "beforeBalance":1.00,
        "cashAmount":1.00,
        "couponAmount":0.00,
        "afterBalance":2.00,
        "storeId":2,
        "referenceId":"NG202506171000117904473395842575",
        "operatorId":"order_create_20230821001",
        "transTime":"2025-06-17T13:43:30.578363603",
        "refundTransId":1,
        "remark":"{\"balance\":1.00,\"cardId\":62,\"cashBalance\":1.00,\"couponBalance\":0.00,\"createTime\":\"2025-06-16 20:48:36\",\"updateTime\":\"2025-06-17 11:41:02.399\",\"userCardId\":62,\"userId\":\"8dd91d41d98f4a7580022044f7502d68\",\"version\":2}"
     },
    "errormsg":null,
    "ok":true
  }


  
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
