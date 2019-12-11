## 配网服务

```java
INetConfigManager iNetConfigManager = IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.NET_CONFIG_SERVICE);

/**
 * 配网服务接口
 */
public interface INetConfigManager {

    void setPID(String pid);

    public void setAuthorKey(String authorKey);

    public void setUserId(String userId);

    /**
     * 检查网络，完成配网过程
     * @param callback 配网回调
     * void configOver(String token); 配网结束回调
     * void startConfig(); 开始配网回调
     * void recConfigInfo(); 设备收到配网信息回调
     */
    void configNetInfo(NetConfigCallback callback);

    /**
     * 配置配网参数
     * @param param
     * @param obj
     */
    void config(String param,Object obj);

    /**
     * 停止配网
     */
    void stop(Context ctx);

}
```