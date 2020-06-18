## 移动侦测

```java
IFeatureManager featureManager = IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.FEATURE_SERVICE);

public interface IFeatureManager {

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
     * @param x 起始坐标x
     * @param y 起始坐标y
     * @param w 起始点横向偏移
     * @param h 起始点纵向偏移
     * */
    void setMotionRegion(int x, int y, int w, int h);

	/**
     * 移动侦测
     * @param pixelData 需要侦测的图像数据， 必须为YUV 格式
     * return motionResult 移动侦测的返回结果 失败返回空数组; 
     * 移动侦测的返回结果数组, motionResult[0]: 侦测是否有结果(1: 有结果 0: 无结果)、(motionResult[1]:motionResult[2]) 侦测结果的坐标
     * */
    int[] detectMotion(ByteBuffer pixelData);

    /**
     * 反初始化移动侦测
     * */
    void releaseMotion();

}
```