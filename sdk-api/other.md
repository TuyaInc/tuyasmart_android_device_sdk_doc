##其他API
### HTTP请求

```java
class TransJNIInterface {
    
    /**
     * IPCHttpResponse {
     * 	int errorCode;
     * 	String result;
     * }
     */
    public IPCHttpResponse httpRequest(String apiName,
                                       String apiVersion, String jsonMsg)
}
```