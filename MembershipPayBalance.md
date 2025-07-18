## 会员管理
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

- **响应成功** (200 同一订单重复支付)：
  ```json
  {
    "traceId":null,
    "code":"202506160956",
    "data":null,
    "errormsg":"订单已支付，请勿重复支付",
    "ok":false
  }
