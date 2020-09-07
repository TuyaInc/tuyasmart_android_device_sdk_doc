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

### 日志本地化

```java
/**
 * 开启本地日志保存，SDK的日志会自动保存在配置路径的文件中
 * @param context 上下文
 * @param logPath 日志保存路径（例子：/sdcard/tuya_log）
 * @param cacheDays 日志缓存天数
 */
IPCSDK.openWriteLog(this, "/sdcard/tuya_log/ipc", 3);

//关闭日志保存，在程序退出时调用
IPCSDK.closeWriteLog();
```

### 自定义DNS解析

```java

interface DNSHandler {
    /**
      * 解析域名 返回ip
      */
    String getIP(String hostname);
}

/**
 * 设置自定义解析处理
 */
IPCServiceManager.getInstance().setDnsHandler(handler);
```