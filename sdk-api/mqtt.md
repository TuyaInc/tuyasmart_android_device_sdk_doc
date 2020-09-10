## **MQTT服务**

```java
IMqttProcessManager mqttProcessManager = IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.MQTT_SERVICE);

/**
 * MQTT消息处理相关
 */
public interface IMqttProcessManager {

    /**
     * mqtt 连接状态变化回调
     * 当sdk 与云端mqtt 连接状态发生变化时，进行的回调
     * */
    void setMqttStatusChangedCallback(IMqttStatusCallback cb);
    
    /**
     * MQTT状态码：
     * */
    public class MqttConnectStatus {
        /**
         * 连接到云端，初始化完成，设备上线
         * */
        public static final int STATUS_CLOUD_CONN = 7;
        /**
         * 与云端断开连接，设备离线
         * */
        public static final int STATUS_OFFLINE = 10;
        /**
         * 设备已经绑定
         * */
        public static final int STATUS_ALREADY_BIND = 9;
    }
    
    /**
     * 开启低功耗模式
     * @param interval 心跳间隔时间（单位秒，设置为120以内）
     * @param callback 唤醒回调
     */
    public boolean enableLowPower(int interval, WakeUpCallback callback);

    /**
     * 关闭低功耗模式
     */
    public boolean disableLowPower();

}
```