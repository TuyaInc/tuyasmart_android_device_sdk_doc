## 移动侦测

```java
IFeatureManager featureManager = IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.FEATURE_SERVICE);

public interface IFeatureManager {

    /**
     * 初始化图像移动侦测
     *
     * @param frame_w         图像宽
     * @param frame_h         图像高
     * @param sensitivity     移动侦测灵敏度，数值越大对应越灵敏 取值范围[1,3]
     * @param y_thd           移动侦测评判阈值，默认30 低照度可降低调试 取值范围[5,30]
     * @param x               侦测区域左上角坐标x所占比例 取值范围[0, 100]
     * @param y               侦测区域左上角坐标y所占比例 取值范围[0, 100]
     * @param w               侦测区域宽所占比例 取值范围[0, 100]
     * @param h               侦测区域高所占比例 取值范围[0, 100]
     * @param tracking_enable 是否进行跟踪 0: 关闭跟踪 1: 开启跟踪
     * @return success: true failed: false
     */
    boolean initMotionDetect(int frame_w, int frame_h, int sensitivity, int y_thd,
                             int x, int y, int w, int h, int tracking_enable);

    /**
     * 设置移动侦测灵阈值
     * 范围[5-30]. 白天光照强烈阈值可以调大，晚上时光线暗，阈值调小
     *
     * @param threshold
     * @return 是否设置成功
     * */
    boolean setMotionThreshold(int threshold);

    /**
     * 设置移动侦测灵敏度
     * 灵敏度范围[1-3], 灵敏度越来越高
     * @param sensitivity
     * @return 是否设置成功
     * */
    boolean setMotionSensitivity(int sensitivity);

    /**
     * 设置移动侦测区域
     * @param x 起始坐标x所占比例 取值范围[0, 100]
     * @param y 起始坐标y所占比例 取值范围[0, 100]
     * @param w 起始点横向偏移所占比例 取值范围[0, 100]
     * @param h 起始点纵向偏移所占比例 取值范围[0, 100]
     * @return 是否设置成功
     * */
    boolean setMotionRegion(int x, int y, int w, int h);

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

    /**
     * 上报门铃事件到涂鸦云端和App端
     * @param notifyType 门铃事件的类型 {@link Common.DOORBELL_NOTIFICATION_TYPE}
     * @param picData 上报事件附带的图片数据
     * @param picType 图片数据格式 {@link Common.NOTIFICATION_CONTENT_TYPE_E}
     * jpeg文件 NOTIFICATION_CONTENT_JPEG，png文件 NOTIFICATION_CONTENT_PNG
     * */
    int notifyDoorBellEvent(int notifyType, byte[] picData, int picType);

   /**
     * 初始化门铃特性相关环境.
     * 若要接受呼叫的接听状态反馈，则必须调用该接口，否则无法接收
     * @return 0: success !0: failed
   * */
    int initDoorBellFeatureEnv();

   /**
     * 销毁门铃特性相关环境.
     * 此方法调用后，门铃相关特性不在可用
     * @return 0: success !0: failed
   * */
    int deInitDoorBellFeatureEnv();

    /**
     * 门铃事件上报
     */
    public class DOORBELL_NOTIFICATION_TYPE {
        public static final int NOTIFICATION_NAME_MOTION = 0;             /* 移动侦测 */
        public static final int NOTIFICATION_NAME_DOORBELL = 1;           /* 门铃按下 */
        public static final int NOTIFICATION_NAME_DEV_LINK = 2;           /* IOT设备联动触发(该类型由云端下发，不能主动触发) */
        public static final int NOTIFICATION_NAME_PASSBY = 3;             /* 正常经过 */
        public static final int NOTIFICATION_NAME_LINGER = 4;             /* 异常逗留 */
        public static final int NOTIFICATION_NAME_MESSAGE = 5;            /* 留言信息 */
        public static final int NOTIFICATION_NAME_CALL_ACCEPT = 6;        /* 门铃接听 */
        public static final int NOTIFICATION_NAME_CALL_NOT_ACCEPT = 7;    /* 门铃未接听 */
        public static final int NOTIFICATION_NAME_CALL_REFUSE = 8;        /* 门铃拒绝接听 */
        public static final int NOTIFICATION_NAME_HUMAN = 9;              /* 人形检测 */
        public static final int NOTIFICATION_NAME_PCD = 10;               /* 宠物检测 */
        public static final int NOTIFICATION_NAME_CAR = 11;               /* 车辆检测 */
        public static final int NOTIFICATION_NAME_BABY_CRY = 12;          /* 婴儿哭声 */
        public static final int NOTIFICATION_NAME_ABNORMAL_SOUND = 13;    /* 声音异响 */
        public static final int NOTIFICATION_NAME_FACE = 14;              /* 人脸检测 */
        public static final int NOTIFICATION_NAME_ANTIBREAK = 15;         /* 强拆告警 */
        public static final int NOTIFICATION_NAME_RECORD_ONLY = 16;       /* 占位，无意义 */
        public static final int NOTIFICATION_NAME_IO_ALARM =17;           /* 本地IO设备触发 */
    }

}
```