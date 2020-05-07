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
     * 自己控制发送心跳包
     */
    public boolean sendHeartbeat();

    /**
     * 主动发送MQTT消息
     * @param protocol  协议编号
     * @param jsonString    消息体
     */
    public void sendMqttMsg(int protocol, String jsonString);

    /**
     * 注册接收MQTT消息
     * @param protocol  协议编号
     * @param callback  消息回调
     * @param <T>   接收消息的类型(MQTT消息结构的data字段)
     */
    public <T> void registerMqttMsg(int protocol, MqttMsgCallback<T> callback);

    /**
     * 反注册
     * @param protocol  协议编号
     */
    public void unregisterMqttMsg(int protocol);

}
```