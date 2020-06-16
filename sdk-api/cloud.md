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
     * @param type          云存储时间类型
     * @param maxDuration   云存储最大时间 单位 (秒)
     * @return 返回一个存储事件 event id
     */
    public int addCloudStorageEvent(byte[] snap_buffer, int snapshot_size, int type, int maxDuration);

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