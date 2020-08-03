## 音视频流

```java

public interface IMediaTransManager {
	
	/**
     * 启动多媒体传输通道.这个方法必须调用，否则无法push 数据流到App端，也无法接受Mqtt消息.
     * (注意： 需要在MQTT上线时开启，请参看文档"SDK初始化-开始推流"部分)
     * 调用这个方法之后，可用通过{@link IMediaTransManager#pushMediaStream(int, int, byte[], long)} 方法push
     * 一帧数据流到该SDK
     * @param max 接收并发量
     * @return success: 0 fase: !0
     * */
    int startMultiMediaTrans(int max);
    
    /**
     * 关闭多媒体传输通道.
     * 该方法调用之后，所有的传输通道都被关闭，多媒体流无法push到client端，也无法接受Mqtt消息
     * @return success: 0 fase: !0
     * */
    int stopMultiMediaTrans();

    /**
     * 关闭多媒体传输通道.
     * 设备端通过该方法可以主动发起呼叫挂断，然后重新开启p2p 通道.
     * 因为关闭通道之后，多媒体流无法push到client端，也无法接受Mqtt消息. 所以，发起主动挂断呼叫之后，需要重新开启此通道.
     * @param max 接收并发量
     * @return success: 0 fase: !0
     * */
    int stopAndRestartMultiMediaTrans(int max);
   
   
   /**
     * 码流通道类型
     * */
    public class Common.ChannelIndex {

        /**
         * 视频流路数
         */
        public static final int E_CHANNEL_VIDEO_MAIN = 0;
        public static final int E_CHANNEL_VIDEO_SUB = 1;
        public static final int E_CHANNEL_VIDEO_3RD = 2;
        public static final int E_CHANNEL_VIDEO_4TH = 3;
        /**
         * 最大支持视频码流路数
         */
        public static final int E_CHANNEL_VIDEO_MAX = 8;

        /**
         * 音频流路数
         */
        public static final int E_CHANNEL_AUDIO = 9;
        public static final int E_CHANNEL_AUDIO_2RD = 10;
        public static final int E_CHANNEL_AUDIO_3RD = 11;
        public static final int E_CHANNEL_AUDIO_4TH = 12;
        /**
         * 最大支持音频码流路数
         * */
        public static final int E_CHANNEL_MAX = 16;
    }
   
       /**
     * push 一帧多媒体流到SDK
     * @param streamType 媒体数据类型 {@link Common.ChannelIndex}
     * @param nalType 是视频流时，为H264码流的nal类型. 是音频流时，此参数无效，默认为0
     * @param streamData 码流数据
     * @return success: 0 fase: !0
     * */
    int pushMediaStream(int streamType, int nalType, byte[] streamData);
    
    /**
     * 注册对讲回调接口
     * 该接口将回调对讲时的音频数据
     * @param cb
     * */
    void addAudioTalkCallback(AudioTalkCallback cb);
    
    interface AudioTalkCallback {
    /**
     * 开启对讲后的数据回调接口
     * @param data 对讲回调数据. 回调之后的数据格式为PCM
     * */
    	void onAudioTalkData(byte[] data);
	}

	/**
     * 注册P2P回调接口
     * */
    void setP2PEventCallback(IP2PEventCallback cb);
    
    interface IP2PEventCallback {
    /**
     * p2p 事件回调
     * @param event 请求事件{@link IMediaTransManager.P2PEvent}
     * @param value 请求事件的值
     * */
    void onEvent(IMediaTransManager.P2PEvent event,Object value);
    
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
        
   /**
     * 设置门铃呼叫状态回调接口
     * 注该接口之后，将接收到门铃呼叫后的接听和挂断状态
     * 门铃呼叫报警接听状态：
     * status = -1 未知状态
     * status = 0 接听
     * status = 1 挂断
     * status = 2 通话中心跳
     * {@link Common.DoorBellCallStatus}
   * */
    void setDoorBellCallStatusCallback(@AutoTestInterface IDoorBellCallStatusCb cb);


    /**
     * 当门铃按下时device端发送门铃呼叫到App端和云端. 此时呼叫界面显示为本地视频画面
     * @param data 发送呼叫时需要附带一张图片
     * @param snapType 图片的类型 {@link Common.NOTIFICATION_CONTENT_TYPE_E}
     * 视频，.mp4文件 NOTIFICATION_CONTENT_MP4
     * 图片，.jpeg文件 NOTIFICATION_CONTENT_JPEG
     * 图片，.png文件 NOTIFICATION_CONTENT_PNG
     * @return 0: success !0: failed
     * */
    int sendDoorBellCallForPress(@Nullable byte[] data, int snapType);
	
}

```