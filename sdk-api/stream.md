## 音视频流

```java

public interface IMediaTransManager {
	
	/**
     * 启动多媒体传输通道.这个方法必须调用，否则无法push 数据流到App端，也无法接受Mqtt消息.
     * 调用这个方法之后，可用通过{@link IMediaTransManager#pushMediaStream(int, int, byte[], long)} 方法push
     * 一帧数据流到该SDK
     * @return success: 0 fase: !0
     * */
    int startMultiMediaTrans();
    
    /**
     * 关闭多媒体传输通道.
     * 该方法调用之后，所有的传输通道都被关闭，多媒体流无法push到client端，也无法接受Mqtt消息
     * */
    int stopMultiMediaTrans();

    /**
     * 关闭多媒体传输通道.
     * 设备端通过该方法可以主动发起呼叫挂断，然后重新开启p2p 通道.
     * 因为关闭通道之后，多媒体流无法push到client端，也无法接受Mqtt消息. 所以，发起主动挂断呼叫之后，需要重新开启此通道.
     * */
    int stopAndRestartMultiMediaTrans();

    /**
     * 启动EchoShow和Chromecast
     * @param videoType 传输的视频流类型 {@link Common.ChannelIndex} 主码流或者为子码流
     *  注意：调用该方法之前，videoType 通道的媒体参数必须已经通过{@link com.tuya.smart.aiipc.ipc_sdk.impl.ParamConfigManager} 设置
     *
     * */
   int startEchoShowAndChromecast(int videoType);
   
       /**
     * push 一帧多媒体流到SDK
     * @param streamType 媒体数据类型 {@link Common.ChannelIndex}
     * @param nalType 是视频流时，为H264码流的nal类型. 是音频流时，此参数无效，默认为0
     * @param streamData 码流数据
     * @param timeStamp 每一帧数据产生的时间戳
     * */
    int pushMediaStream(int streamType, int nalType, byte[] streamData, long timeStamp);
    
    /**
     * 注册对讲回调接口
     * 该接口将回调对讲时的音频数据
     * @param cb
     * */
    void addAudioTalkCallback(AudioTalkCallback cb);

	/**
     * 注册P2P回调接口
     * */
    void setP2PEventCallback(IP2PEventCallback cb);
    
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
	
}

```