## 云存储

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