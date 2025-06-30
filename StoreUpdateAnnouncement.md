## 会员管理
### 门店变更通知
- **URL**：`/third-api/open/v1/third/orderChange`
- **Method**：`POST`
- **json Body 参数**：
  | 参数     | 必填 | 说明      |
  |------    |------|-----------|
  | orderSn   | 是   | 订单号   |
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
      https://testalb.jicaoge.com/third-api/open/v1/third/orderChange

    --POST data--:
      {
        "orderSn":"NG202506171000117904473395842575",
        "storeId":82374
      }

    X-Third-Authorization: nonce_str="dszvrLhgzs4gxdKGtsc2OMR4Cue4fT0z",signature="m2Y3T4cxfTWYWPBh5F0TFjLJKYA4a2y2+HQrEKwxQN7QGSUuPxJVUGHLlunlHDNXsuDdh3GPmGBHjSm4V82Mcfzbu7PKIZ2W7lCrYcGiHop6vK1dIqQFeq4OjROkrB95kfSDsiAGQzPiEr2iTwmJXh5fWiWZE+PgLSXYykot6wkCd8bkjJKpwYHSbUDCCX95xGEUrcTg6Dg77yDel6Bujt0YXQpxy6vIlJUcTCCJrYdFzm/TI3W7ilxxfkrvtYR4r9yckb5dmu0OwNZEG1zQjOwft40rjH9pJMlRP4BiXNJR6/dqRe6Ne23IrA/h+I5tWBBhom08JRwTVeC6Tu+rkw==",timestamp="1751252398",serial_no="store001"

```
- **响应成功** (200)：
  ```json
  {
    "traceId":null,
    "code":"200",
    "data":null,
    "errormsg":null,
    "ok":true
  }
