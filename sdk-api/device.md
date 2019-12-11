## 设备相关信息

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