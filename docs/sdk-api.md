# SDK API

## **通用API**

> 不需要接入IPC

### **MQTT服务**

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

## **IPC API**

> **需要接入IPC**

### 配网服务

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

### <div id="dp">DP控制</div>

```java
IControllerManager controllerManager = IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.CONTROLLER_SERVICE);

public interface IControllerManager {

    /**
     * dp上报接口，在处理完dp点之后回复客户端
     * @param dpID dp标示
     * @param type 类型
     * @param pVal 值
     * @return
     */
    int dpReport(int dpID, int type, Object pVal);
    
    /**
     * 基础的DP回调类
     *
     * @param dpEventSimpleCallback
     */
    void setDpEventSimpleCallback(DPEventSimpleCallback dpEventSimpleCallback);

    /**
     * 复杂的DP处理类
     *
     * @param callback
     */
    void setDPEventCallback(AbstractDPEventCallback callback);

}

//dp点定义
public class DPEvent {

    /**
     *  状态指示灯,BOOL类型,true打开,false关闭
     */
    public static final int TUYA_DP_LIGHT = 101;
    /**
     * 录制画面翻转,BOOL类型,true反转,false正常
     */
    public static final int TUYA_DP_FLIP = 103;
    /**
     * 视频水印,BOOL类型,true打开水印,false关闭水印
     */
    public static final int TUYA_DP_WATERMARK = 104;

    /**
     * type
     */
    /**
     *  休眠,BOOL类型,true休眠,false不休眠
     */
    public static final int TUYA_DP_SLEEP_MODE = 105;

    /**
     * 移动侦测报警灵敏度,ENUM类型,0为低灵敏度,1为中灵敏度,2为高灵敏度 {@link com.tuya.smart.aiipc.ipc_sdk.callback.DPConst.AlarmSensitivity}
     */
    public static final int TUYA_DP_ALARM_SENSITIVITY = 106;

    /**
     * 宽动态范围模式,BOOL类型,true则打开宽动态范围模式,false则关闭宽动态范围
     */
    public static final int TUYA_DP_WDR = 107;

    /**
     * 红外夜视功能,ENUM类型,0-自动 1-关 2-开 {@link com.tuya.smart.aiipc.ipc_sdk.callback.DPConst.NightMode}
     */
    public static final int TUYA_DP_NIGHT_MODE = 108;

    /**
     *  SD卡容量,STR类型,"总容量|当前使用量|剩余容量",单位：kb
     */
    public static final int TUYA_DP_SD_STORAGE_ONLY_GET = 109;

    /* APP储存卡设置页面 */
    /**
     * SD卡状态,VALUE类型,1-正常,2-异常,3-空间不足,4-正在格式化,5-无SD卡 {@link com.tuya.smart.aiipc.ipc_sdk.callback.DPConst.SDCardStatus}
     */
    public static final int TUYA_DP_SD_STATUS_ONLY_GET = 110;

    /**
     * 格式化存储卡,BOOL类型
     */
    public static final int TUYA_DP_SD_FORMAT = 111;

    /**
     * 退出存储卡,BOOL类型,true为存储卡已退出,false为存储卡未退出
     */
    public static final int TUYA_DP_SD_UMOUNT = 112;


    /**
     * 移动侦测消息报警
     */
    public static final int TUYA_DP_MOTION_DETECTION_ALARM = 115;

    /**
     * 云台转动停止,BOOL类型
     */
    public static final int TUYA_DP_PTZ_STOP = 116;

    /**
     * 格式化存储卡状态,VALUE类型,-2000:SD卡正在格式化,-2001:SD卡格式化异常,-2002:无SD卡,-2003:SD卡错误.正数为格式化进度 {@link com.tuya.smart.aiipc.ipc_sdk.callback.DPConst.FormatStatus}
     */
    public static final int TUYA_DP_SD_FORMAT_STATUS_ONLY_GET = 117;

    /* APP摄像头控制页面 */
    /**
     * 云台转动开始,ENUM类型,0-上,1-右上,2-右,3-右下,4-下,5-左下,6-左,7-左上  {@link com.tuya.smart.aiipc.ipc_sdk.callback.DPConst.PTZControl}
     */
    public static final int TUYA_DP_PTZ_CONTROL = 119;

    /**
     * 摄像机校准,BOOL类型
     */
    public static final int TUYA_DP_CALIBRATION = 132;
    /* APP移动侦测报警页面 */
    /**
     * 移动侦测报警功能开关,BOOL类型,true打开,false关闭
     */
    public static final int TUYA_DP_ALARM_FUNCTION = 134;

    /* IPC特殊功能 */
    /**
     * 门铃呼叫,STR类型,"当前时间戳"
     */
    public static final int TUYA_DP_DOOR_BELL = 136;
    /**
     * 特殊灯光控制开关,BOOL类型,true打开,false关闭
     */
    public static final int TUYA_DP_BLUB_SWITCH = 138;
    /**
     * 分贝检测功能开关,BOOL类型,true打开,false关闭
     */
    public static final int TUYA_DP_SOUND_DETECT = 139;
    /**
     * 分贝检测灵敏度,ENUM类型,0代表低灵敏度,1代表高灵敏度 {@link com.tuya.smart.aiipc.ipc_sdk.callback.DPConst.SoundSensitivity}
     */
    public static final int TUYA_DP_SOUND_SENSITIVITY = 140;
    /**
     * 分贝报警通道,STR类型,"当前时间戳"
     */
    public static final int TUYA_DP_SOUND_ALARM = 141;
    /**
     * 温度检测,VALUE类型,[0-50]
     */
    public static final int TUYA_DP_TEMPERATURE = 142;
    /**
     * 湿度检测,VALUE类型,[0-100]
     */
    public static final int TUYA_DP_HUMIDITY = 143;
    /**
     * 电池电量(百分比),VALUE类型,[0-100]
     */
    public static final int TUYA_DP_ELECTRICITY = 145;
    /**
     * 供电方式,ENUM类型,"0"为电池供电状态,"1"为插电供电状态(或电池充电状态)   {@link com.tuya.smart.aiipc.ipc_sdk.callback.DPConst.PowerMode}
     */
    public static final int TUYA_DP_POWERMODE = 146;
    /**
     * 低电告警阈值(百分比),VALUE类型
     */
    public static final int TUYA_DP_LOWELECTRIC = 147;

    /**
     * SD卡录像功能使能,BOOL类型,true打开,false关闭
     */
    public static final int TUYA_DP_SD_RECORD_ENABLE = 150;
    /**
     * SD卡录像模式选择,ENUM类型,1-事件录像 2-连续录像 {@link com.tuya.smart.aiipc.ipc_sdk.callback.DPConst.SDRecordMode}
     */
    public static final int TUYA_DP_SD_RECORD_MODE = 151;

    /**
     * 门铃-抓拍图片
     */
    public static final int TUYA_DP_DOOR_BELL_SNAP = 154;


    //AI
    /**
     * 移动侦测报警区域开关
     */
    public static final int TUYA_DP_MOTION_AREA_SWITCH = 168;
    /**
     * 移动侦测报警区域
     */
    public static final int TUYA_DP_MOTION_AREA = 169;
    /**
     * 人行过滤
     */
    public static final int TUYA_DP_HUMANOID_FILTER = 170;
    /**
     * 告警消息-上报
     */
    public static final int TUYA_DP_ALARM_MESSAGE = 185;
    /**
     * AI人脸识别开关
     */
    public static final int TUYA_DP_AI_FR_SWITCH = 186;



}

```

### 设备相关信息

```java
IDeviceManager deviceManager = IPCServiceManager
.getInstance().getService(IPCServiceManager.IPCService.DEVICE_SERVICE);

public interface IDeviceManager {

    /**
     * 获取DP点 SDCard状态  {@link com.tuya.smart.aiipc.ipc_sdk.callback.DPConst.SDCardStatus}
     */
    int getDPSDCardStatus();

    /**
     * 获取SDCard格式化状态
     */
    int getSDCardFormatStatus();

    /**
     * 格式化SDCard
     */
    void SDCardFormat();

    /**
     * 重新挂载SDCard
     */
    void SDCardRemount();

    /**
     * SDK获取SDCard {@link SDStatus}
     */
    int SDCardGetStatus();

    /**
     * 获取SDCard容量
     */
    SDVolumeInfo SDCardGetCapacity();

    /**
     * 获取SDCard路径
     */
    String SDCardMountPath();

    /**
     * SD卡文件录入的方式
     */
    int GetModeConfig();

    /**
     * 获取设备ID
     */
    String getDeviceId();

}
```

### <div id="移动侦测">移动侦测</div>

```java
IFeatureManager featureManager = IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.FEATURE_SERVICE);

public interface IFeatureManager {

    /**
     * 设置上传视频开关
     * @param on
     */
    void setUploadVideo(boolean on);

    /**
     * 设置存储事件
     * @param type
     */
    void setStoryType(StoreType type);

    /**
     * 初始化图像移动侦测
     * @param frame_w 图像宽
     * @param frame_h 图像高
     * @param sensitivity 移动侦测灵敏度，设置1-3,对应越来越灵敏
     * @param y_thd 移动侦测评判阈值，默认30 低照度可降低调试
     * @param x 侦测区域左上角坐标x
     * @param y 侦测区域左上角坐标y
     * @param w 侦测区域宽
     * @param h 侦测区域高
     * @param tracking_enable 是否进行跟踪 0: 关闭跟踪 1: 开启跟踪
     *
     * @return success: true failed: false
     * */
    boolean initMotionDetect(int frame_w, int frame_h, int sensitivity, int y_thd,
                             int x, int y, int w, int h, int tracking_enable);

    /**
     * 设置移动侦测图片分辨率
     * @param frame_w
     * @param frame_h
     * */
    void setMotionFrameSize(int frame_w, int frame_h);

    /**
     * 设置移动侦测灵阈值
     * 范围[5-30]. 白天光照强烈阈值可以调大，晚上时光线暗，阈值调小
     *
     * @param threshold
     * */
    void setMotionThreshold(int threshold);

    /**
     * 设置移动侦测灵敏度
     * 灵敏度范围[1-3], 灵敏度越来越高
     * @param sensitivity
     * */
    void setMotionSensitivity(int sensitivity);

    /**
     * 设置移动侦测区域
     * @param index 区域index
     * @param x 起始坐标x
     * @param y 起始坐标y
     * @param w 起始点横向偏移
     * @param h 起始点纵向偏移
     * */
    void setMotionRegion(int index, int x, int y, int w, int h);

    /**
     * 移动侦测
     * @param pixelData 需要侦测的图像数据， 必须为YUV 格式
     * @param motionResult 移动侦测的返回结果 motionResult[0]: 侦测是否有结果(1: 有结果 0: 无结果)
     *                     (motionResult[1]:motionResult[2]) 侦测结果的坐标
     * return success: 1 failed: !1 */
    int detectMotion(ByteBuffer pixelData, int[] motionResult);

    /**
     * 反初始化移动侦测
     * */
    void releaseMotion();

}
```

### *低功耗模式（标准版暂未包含）

```java
class TransJNIInterface {
    
    /**
     * 进入低功耗
     *
     * @param interval 心跳间隔30-120s，默认60s,如果小于0则不发送
     * @param callback app唤醒的回调
     * @return
     */
    public boolean enableLowPower(int interval, WakeUpCallback callback);


    /**
     * 退出低功耗
     *
     * @return
     */
    public boolean disableLowPower();
    
}
```

### <div id="P2P">P2P</div>

```java
class TransJNIInterface {
    
     /**
     * 启动 P2P 传输模块
     */
    public int startMultiMediaTrans();

    /**
     * 停止P2P 传输
     */
    public int closeMultiMediaTrans();
    
    /**
     * 设置P2P事件回调
     * @param P2PEventCallback: callback of P2PEvent
     * 
     */
    public void setP2pEventCallback(P2PEventCallback cb);
}

//p2p事件定义
enum P2PEvent{
        UNKNOW(-1),
        TRANS_LIVE_VIDEO_START(0),  /**video 直播开始请求*/
        TRANS_LIVE_VIDEO_STOP(1),   /**video 直播结束结束*/
        TRANS_LIVE_AUDIO_START(2),  /**audio 直播开始请求*/
        TRANS_LIVE_AUDIO_STOP(3),   /**audio 直播开始请求*/

        TRAN_VIDEO_CLARITY_SET(4), /**< 设置视频直播清晰度 ，参数为*/

        TRANS_SPEAKER_START(16),   /**对讲请求 */
        TRANS_SPEAKER_STOP(17);
        }
```

### 云存储

```java
IMediaTransManager transManager = IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.MEDIA_TRANS_SERVICE);

public interface IMediaTransManager {

    /**
     * 开启/暂停/恢复 云存储
     * @return 返回一个存储事件 event id
     */
    public int startCloudStorage();
    
    public int pauseCloudStorage();

    public int resumeCloudStorage();

    /**
     * 启动一个云存储事件.
     *
     * @param snap_buffer   jpeg 数据, 大小不超过100k
     * @param snapshot_size
     * @param type          云存储时间类型
     * @return 返回一个存储事件 event id
     */
    public int startCloudStorageEvent(byte[] snap_buffer, int snapshot_size, int type);

    /**
     * 停止一个云存储事件
     *
     * @param eventId #addCloudStorageEvent 返回的云存储事件id
     */
    public int stopCloudStorageEvent();
    
     /**
     * 添加一个云存储事件.
     *
     * @param snap_buffer   jpeg 数据, 大小不超过100k
     * @param snapshot_size
     * @param type          云存储时间类型
     * @param maxDuration   云存储最大时间 单位 (秒)
     * @return 返回一个存储事件 event id
     */
    public int addCloudStorageEvent(byte[] snap_buffer, int snapshot_size, int type, int maxDuration);

    /**
     * 删除一个云存储事件
     *
     * @param eventId #addCloudStorageEvent 返回的云存储事件id
     */
    public int deleteCloudStorageEvent(int eventId);

    /**
     * 获取云存储订单类型 {@see CloudStorageType}
     */
    public int getCloudStorageStoreMode();

    /**
     * 获取云存储事件状态 
     * @param type
     * @return {@see Common.EventStatus}
     */
    public int getCloudStorageEventStatus(int type);
    
}
```

### 视频流

```java
class TransJNIInterface {
    
     /**
     * push 一帧数据流
     *
     * @param streamType
     * @param nalType
     * @param streamData
     * @param timeStamp
     */
    public int pushMediaStream(int streamType, int nalType, byte[] streamData, long timeStamp);
    
}
```

### HTTP请求

```java
class TransJNIInterface {
    
    public IPCHttpResponse httpRequest(String apiName,
                                       String apiVersion, String jsonMsg)
}
```

