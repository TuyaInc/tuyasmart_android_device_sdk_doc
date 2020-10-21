## <div id="dp">DP控制</div>

```java
IControllerManager controllerManager = IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.CONTROLLER_SERVICE);

public interface IControllerManager {

    /**
     * dp上报接口，在处理完dp点之后回复客户端
     * @param dpID dp标示
     * @param type 类型
     * Boolean DPConst.Type.PROP_BOOL
     * Integer DPConst.Type.PROP_VALUE
     * String DPConst.Type.PROP_STR
     * Enum DPConst.Type.PROP_ENUM
     * Bitmap DPConst.Type.PROP_BITMAP
     * @param pVal 值
     * @return
     */
    int dpReport(int dpID, int type, Object pVal);
    
    /**
     * DP回调类
     *
     * @param dpEventSimpleCallback
     */
    void setDpEventSimpleCallback(DPEventSimpleCallback dpEventSimpleCallback);

    public interface DPEventSimpleCallback {

        /**
         * dp接收
         * @param v 值
         * @param dpid dpid
         * @param time_stamp 时间戳
         * @return
         */
        DPConst.DPResult onDPEvent(Object v, int dpid, long time_stamp);

    }

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