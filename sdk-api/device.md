## 设备相关信息

> 注意：当前页面的方法 SDK只提供默认实现，接入时需要自己实现。

```java
IDeviceManager deviceManager = IPCServiceManager
.getInstance().getService(IPCServiceManager.IPCService.DEVICE_SERVICE);

public interface IDeviceManager {

    /**
     * 获取DP点 SDCard状态  {@link com.tuya.smart.aiipc.ipc_sdk.callback.DPConst.SDCardStatus}
     *	SDCardStatus.NORMAL 正常
     *	SDCardStatus.EXCEPTION 异常
     *	SDCardStatus.OUTOFSPACE 空间不足
     *	SDCardStatus.FORMATING 正在格式化
     *	SDCardStatus.NO_SDCARD 无SD卡
     */
    int getDPSDCardStatus();

    /**
     * 获取SDCard格式化进度（0 ~ 100）
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
     * SD卡状态
     */
    class SDStatus {
        public static final int SD_STATUS_UNKNOWN = 0;
        public static final int SD_STATUS_NORMAL = 1;
        public static final int SD_STATUS_ABNORMAL = 2;
        public static final int SD_STATUS_LACK_SPACE = 3;
        public static final int SD_STATUS_FORMATING = 4;
        public static final int SD_STATUS_NOT_EXIST = 5;
        public static final int SD_STATUS_MAX = 6;
    }

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
     * @return {@link StreamStorageWriteMode}
     */
    int GetModeConfig();
    
    /**
     * SD卡文件录入的方式
     */
    class StreamStorageWriteMode {
        /**
         *  不写入SD卡
         */
        public static final int SS_WRITE_MODE_NONE = 0;

        /**
         *  事件发生时写入SD卡
         */
        public static final int SS_WRITE_MODE_EVENT = 1;

        /**
         * 全时写入SD卡
         */
        public static final int SS_WRITE_MODE_ALL = 2;
    }

    /**
     * 获取设备ID
     */
    String getDeviceId();

}
```