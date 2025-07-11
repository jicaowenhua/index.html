## 订单管理
### 获取取货订单信息
- **URL**：`/third-api/open/v1/third/getUserOrder`
- **Method**：`POST`
- **json Body 参数**：
  | 参数     | 必填 | 说明      |
  |------    |------|-----------|
  | userId   | 是   | 用户 ID   |
  | token   | 是   |  取货码  |
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
      https://testalb.jicaoge.com/third-api/open/v1/third/getUserOrder

    --POST data--:
      {
        "token": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJQRzIwMjUwNzA5MTUxNTMyOTY1NjY5NzUxNjIyMDQyMiIsInJuZCI6ImU3NTgyNTExMTFkZDRiZjJhNTExYjcwYjIzZDNmMjQ5IiwiZXhwIjoxNzUyMjAyNjAyLCJpYXQiOjE3NTIyMDI1Njd9.nDGrXg8NcBRv2yweiiGkfqVCZk3baYvWc4ewZbIHuDs",
        "userId": "8dd91d41d98f4a7580022044f7502d68"
      }

      X-Third-Authorization: nonce_str="R1DNZs9dkpFDL6CknhT5h7bq7AXZVYW2",signature="CbwNRCc2EVfGs1TjSzJoVGOrXZTpxpnrAo1T3CN+xmgbLVjBDs6L+y3YbQCav8deTCoKJvHyXv/OPoF9gbipUcfZsUQmuFoOa9jjrY6FU2+YC9LNL3MFlal0MXI3RvPNUIqhDPHltBH70l+0UWr7gETf3FSDH5U31CwrzF18G6N1eAGZVDy0X+dUb4BAVCLD1N/O+keABOSPi9FzM6EAYIi35XvGsPX2nmTddIkRfAc6cuEDj1uwP8fOFM0YNlw3CNzShZQ8h2GqXGRP7nqTCh3qiJ/UpXYOrf5jcQG/h36AmVe6/tedE7pVk/iUVrCg+moXW/rLUh3GVtN5K59tJQ==",timestamp="1752202573",serial_no="store001"
```
- **响应成功** (200)：
  ```json
    {
      "traceId":null,
      "code":"200",
      "data":"S2025070915000001",
      "errormsg":null,
      "ok":true
    }
