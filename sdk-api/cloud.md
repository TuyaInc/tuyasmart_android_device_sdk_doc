## 云存储

> 说明：  
> 1. 连续存储：调用startCloudStorage，只会打开云端的云存储开关，不会向云端推视频。当前没有推流就没有保存，一旦开始推流了，就会保存。  
2. 事件存储：调用addCloudStorageEvent，会上报云存储事件，也会保存云存储视频（如果已经使用了startCloudStorage开启了连续存储）；调用deleteCloudStorageEvent，会结束云存储事件，也会停止保存云存储视频（如果已经使用了startCloudStorage）


```java
IMediaTransManager transManager = IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.MEDIA_TRANS_SERVICE);

public interface IMediaTransManager {

    /**
     * 开启/暂停/恢复 云存储（连续存储）
     * @return 返回一个存储事件 event id
     */
    public int startCloudStorage();
    
    public int pauseCloudStorage();

    public int resumeCloudStorage();
    
     /**
     * 启动一个云存储事件（事件存储）
     *
     * @param snap_buffer   jpeg 数据, 大小不超过100k
     * @param snapshot_size
     * @param type 云存储事件类型 {@link Common.DOORBELL_NOTIFICATION_TYPE}
     * @param maxDuration   云存储最大时间 单位 (秒)
     * @return 返回一个存储事件 event id
     */
    public int addCloudStorageEvent(byte[] snap_buffer, int snapshot_size, int type, int maxDuration);

    /**
    * 门铃事件上报
    * */
    public class Common.DOORBELL_NOTIFICATION_TYPE {
        public static final int NOTIFICATION_NAME_MOTION = 0;             /* 移动侦测 */
        public static final int NOTIFICATION_NAME_DOORBELL = 1;           /* 门铃按下 */
        public static final int NOTIFICATION_NAME_DEV_LINK = 2;           /* IOT设备联动触发 */
        public static final int NOTIFICATION_NAME_PASSBY = 3;             /* 正常经过 */
        public static final int NOTIFICATION_NAME_LINGER = 4;            /* 异常逗留 */
        public static final int NOTIFICATION_NAME_MESSAGE = 5;            /* 留言信息 */
        public static final int NOTIFICATION_NAME_CALL_ACCEPT = 6;       /* 门铃接听 */
        public static final int NOTIFICATION_NAME_CALL_NOT_ACCEPT = 7;    /* 门铃未接听 */
        public static final int NOTIFICATION_NAME_HUMAN = 8;              /* 人形检测*/
    }

    /**
     * 停止一个云存储事件（事件存储）
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