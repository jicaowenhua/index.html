# 集草开放平台接口文档
## 请求加密规则
```
HTTP请求方法\n
URL\n
请求时间戳\n
请求随机串\n
请求报文主体\n
```
例如请求接口：/open/v1/third/user/verifyToken
POST\n  
/open/v1/third/user/verifyToken\n  
1554208460\n  
593BEC0C930BF1AFEB40B4A08C8FB242\n  
{"token":"eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJjZDQyMTY2MTExZjk0YWY3ODQ5ZDY5Nzk3MGFlNjU1MCIsInJuZCI6IjcwMTI0NjVmLTcwN2EtNDVlNy1iZDdjLTMwOWM2OGYzM2U4NiIsImV4cCI6MTc0OTU0Njg1MCwiaWF0IjoxNzQ5NTQ2ODIwfQ.mKmGP29cUYTKx8qi3QOEGo8GUJKr35cuQzaje1aHfXo"}\n  
实际内容：
```
POST\n/open/v1/third/user/verifyToken\n1554208460\n593BEC0C930BF1AFEB40B4A08C8FB242\n{"token":"eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJjZDQyMTY2MTExZjk0YWY3ODQ5ZDY5Nzk3MGFlNjU1MCIsInJuZCI6IjcwMTI0NjVmLTcwN2EtNDVlNy1iZDdjLTMwOWM2OGYzM2U4NiIsImV4cCI6MTc0OTU0Njg1MCwiaWF0IjoxNzQ5NTQ2ODIwfQ.mKmGP29cUYTKx8qi3QOEGo8GUJKr35cuQzaje1aHfXo"}\n
```
```java

    /**
     * 执行方法
     */
    public void show() throws ParseException {
        String nonce = UUID.randomUUID().toString().replace("-", "");
        String timestamp = String.valueOf(LocalDateTime.now()
                                                       .atZone(ZoneId.systemDefault())
                                                       .toEpochSecond());
        String token = "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJjZDQyMTY2MTExZjk0YWY3ODQ5ZDY5Nzk3MGFlNjU1MCIsInJuZCI6IjcwMTI0NjVmLTcwN2EtNDVlNy1iZDdjLTMwOWM2OGYzM2U4NiIsImV4cCI6MTc0OTU0Njg1MCwiaWF0IjoxNzQ5NTQ2ODIwfQ.mKmGP29cUYTKx8qi3QOEGo8GUJKr35cuQzaje1aHfXo";
        JSONObject object = new JSONObject();
        object.put("token", token);
        String body = object.toJSONString();
        String signedBody = buildSignedBody(timestamp, nonce, body);
        String authorization = signData(signedBody);
        JsapiTransactionResponse response = jsapi(authorization, "application/json", body);
    }


    private String buildSignedBody(String timestamp, String nonce_str, String body) {
        return "POST\n" +
                "/open/v1/third/user/verifyToken\n" +
                timestamp + "\n" +
                nonce_str + "\n" +
                body + "\n";
    }

    public String signData(String data) {
        try {
            PrivateKey privateKey = rsaKeyManager.getPrivateKey();
            if (privateKey == null) {
                throw new IllegalStateException("Private key is not initialized.");
            }

            Signature signature = Signature.getInstance("SHA256withRSA");
            signature.initSign(privateKey);
            signature.update(data.getBytes(StandardCharsets.UTF_8));

            return Base64.getEncoder()
                         .encodeToString(signature.sign());
        } catch (Exception e) {
            throw new RuntimeException("Failed to sign data.", e);
        }
    }

    /**
     * 调用集草平台
     */
    @PostMapping(value = "/open/v1/third/user/verifyToken", consumes = MediaType.APPLICATION_JSON_VALUE)
    JsapiTransactionResponse jsapi(@RequestHeader("Authorization") String authorization,
                                   @RequestHeader("Accept") String accept,
                                   @RequestBody String body);
```

