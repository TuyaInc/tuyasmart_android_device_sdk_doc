# FAQ
### **如何配置视频/音频参数**

```java
IParamConfigManager configManager = IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.MEDIA_PARAM_SERVICE);

configManager.setInt(int channelIndex, String key, int value);
```
> 可配置参数请查看 Common.ParamKey

```java
//example

//主码流设置帧数
configManager.setInt(Common.ChannelIndex.E_CHANNEL_VIDEO_MAIN, Common.ParamKey.KEY_VIDEO_FRAME_RATE, 24);

//子码流设置I帧间隔
configManager.setInt(Common.ChannelIndex.E_CHANNEL_VIDEO_SUB, Common.ParamKey.KEY_VIDEO_I_FRAME_INTERVAL, 2);

//主音频流设置采样率
configManager.setInt(Common.ChannelIndex.E_CHANNEL_AUDIO, Common.ParamKey.KEY_AUDIO_SAMPLE_RATE, 8000);
```

### **怎么开启视频流传输**

> 请查看[初始化文档 “开始推流”部分](./sdk-chu-shi-hua.md#开始推流)

### **如何获得语音数据**

```java
IMediaTransManager transManager = IPCServiceManager.getInstance().getService(IPCServiceManager.IPCService.MEDIA_TRANS_SERVICE);
transManager.addAudioTalkCallback(new AudioTalkCallback() {
                    @Override
                    public void onAudioTalkData(byte[] data) {
                    	//处理音频数据
                    }
                });
```

### **如何传递信号强度**

```java
IControllerManager controllerManager = IPCServiceManager.getInstance().getService(IPCServiceManager.IPCService.CONTROLLER_SERVICE);

//设置信号值
controllerManager.setQueryCallback(event -> {
	if (event == IMediaTransManager.QueryEvent.QUERY_RSSI) {
	//信号
	return 50;
	}
});
```
### **如何知道app是否在看视频**

> 通过[P2P API](./sdk-api/stream.md)获取回调

### **心跳时间多长**

> 60s

### **我的设备不支持蓝牙有影响吗**

> 不能使用蓝牙配网功能

### **我正常的h264格式怎么播放不出来**

> 需要使用特定的编码格式，即保证每一个IDR帧前有SPS和PPS  
> 可以参考demo中的类 `H264FileVideoCapture`

### **怎么一直显示正在获取流**

> 可能是p2p打洞失败，重启涂鸦智能app试试。

### **加密通道构建失败是什么情况**

> APP端看下设备是否离线，离线需要重连设备。如果在线则尝试退出设备面板重进。

### **如何发送警报或者移动侦测**

> [移动侦测API](./sdk-api/motion.md)

<!--### **怎么发起视频通话**-->

### **怎么处理dp点，定义怎么看**

> 请查看[DP API](./sdk-api/dp.md)

### **系统存储跟我系统的显示不一样，怎么自定义系统存储**

> 请查看[设备管理 API](./sdk-api/device.md)，自定义实现接口方法，替换设备管理服务（[如何替换服务](./sdk-api/README.md#服务替换)）。

### **语音的数据是什么格式的，需要怎么去播放**

> 格式为PCM, 使用AudioTrack播放。

###扫码配网的预览相机可以配置么

```java
iNetConfigManager.config(INetConfigManager.QR_PARAMETERS, (INetConfigManager.OnParameterSetting) (parameters, camera) -> {
			  //Camera.Parameters p, Camera mCamera
            	camera.setDisplayOrientation(90);
        });

```

###API如何查询

> 可以在SDK API分级目录里找到需要的功能，找不到可以尝试文档搜索。

