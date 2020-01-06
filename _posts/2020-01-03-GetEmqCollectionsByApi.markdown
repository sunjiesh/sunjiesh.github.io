---

layout: post 
title: "通过API读取Emq Connections" 
date: 2020-01-03 17:40:00 +0800
categories: Java
---

主要代码如下

```java

	private List<JSONObject> getCollections() {
        try {

            String plainText = emqApiId + ":" + emqAppSecret;
            String encode = new Base64().encodeToString(plainText.getBytes());
            HttpClient httpClient = new DefaultHttpClient();
            String getConnectionsUrl = String.format("%s/api/v3/connections/", emqApiUrl);
            HttpGet httpGet = new HttpGet(getConnectionsUrl);
            httpGet.setHeader("Authorization", "Basic " + encode);
            HttpResponse httpResponse = httpClient.execute(httpGet);
            StatusLine statusLine = httpResponse.getStatusLine();
            int statusCode = statusLine.getStatusCode();
            if (statusCode != 200) {
                LOGGER.error("Get connections failure");
                return null;
            }
            HttpEntity respEntity = httpResponse.getEntity();
            String respStr = EntityUtils.toString(respEntity);
            LOGGER.info("respStr is = {}", respStr);
            JSONObject respJson = JSONObject.parseObject(respStr);
            if (respJson == null) {
                LOGGER.error("Get connections failure,reason is null");
                return null;
            }
            int code = respJson.getIntValue("code");
            if (code != 0) {
                LOGGER.error("Get connections failure,code is err");
                return null;
            }
            List<JSONObject> result = new ArrayList<JSONObject>();
            JSONArray dataJsonArr = respJson.getJSONArray("data");
            for (int index = 0; index < dataJsonArr.size(); index++) {
                JSONObject dataJson = dataJsonArr.getJSONObject(index);
                result.add(dataJson);
            }
            return result;

        } catch (Exception e) {
            LOGGER.error(e.getMessage(), e);
        }
        return null;
    }
```
