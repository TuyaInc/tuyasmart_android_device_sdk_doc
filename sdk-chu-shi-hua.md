# SDK初始化

> 提示：接入和使用可能遇到的一些常见问题，在<a href="./faq.md">FAQ</a>都有记录，遇到困难可以先查看一下：）

## 依赖配置
```groovy
maven { url 'https://maven-other.tuya.com/repository/maven-releases/'}
maven { url 'https://maven-other.tuya.com/repository/maven-snapshots/'}
```

```groovy
implementation 'com.tuya.smart:tuyasmart-ipc_sdk:1.0.5'

implementation 'com.android.support:appcompat-v7:28.0.0'
implementation 'com.google.code.gson:gson:2.8.5'
implementation 'com.alibaba:fastjson:1.1.67.android'
implementation 'com.google.zxing:core:3.3.0'
implementation 'com.tencent.mars:mars-xlog:1.2.3'
```

```groovy
packagingOptions {
    pickFirst 'lib/armeabi-v7a/libc++_shared.so'
}

compileOptions {
        sourceCompatibility = '1.8'
        targetCompatibility = '1.8'
    }
```

## 防混淆
```groovy
-keep class com.tuya.** {*;}
-keep com.tencent.mars.** {*;}
```

## 权限配置

```markup
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
```

## 初始化流程

### **1.初始化SDK**

```java
IPCSDK.initSDK(this);
```

### **2.设置流的配置**

**配置参数**

```java
package com.tuya.smart.aiipc.ipc_sdk.api;

public class Common {

    /**
     * 码流通道类型
     * */
    public class ChannelIndex {

        public static final int E_CHANNEL_VIDEO_MAIN = 0;
        public static final int E_CHANNEL_VIDEO_SUB = 1;
        public static final int E_CHANNEL_VIDEO_3RD = 2;
        public static final int E_CHANNEL_VIDEO_4TH = 3;
        public static final int E_CHANNEL_VIDEO_MAX = 8;    //最大支持视频码流路数
        public static final int E_CHANNEL_AUDIO = 9;
        public static final int E_CHANNEL_AUDIO_2RD = 10;
        public static final int E_CHANNEL_AUDIO_3RD = 11;
        public static final int E_CHANNEL_AUDIO_4TH = 12;
        public static final int E_CHANNEL_MAX = 16;
    }

    /**
     * 时间类型
     * */
    public class EventType {
        public static final int EVENT_TYPE_MOTION_DETECT = 0;  /* 移动侦测触发的存储 */
        public static final int EVENT_TYPE_DOOR_BELL = 1;       /* 门铃唤醒触发的存储 */
        public static final int EVENT_TYPE_INVALID = 2;
    }

    /**
     * 传输特定的NAL 类型
     * */
    public class NAL_TYPE {
        public static final int NAL_TYPE_IDR = 3;
        public static final int NAL_TYPE_PB = 4;
    }

    /**
     * 上报数据类型
     * */
    public class NOTIFICATION_CONTENT_TYPE_E {
        public static final int NOTIFICATION_CONTENT_MP4 = 0; /* 视频，.mp4文件 */
        public static final int NOTIFICATION_CONTENT_JPEG = 1; /* 图片，.jpeg文件 */
        public static final int NOTIFICATION_CONTENT_PNG = 2; /* 图片，.png文件 */
        public static final int NOTIFICATION_CONTENT_MAX = 3;
    }

    public class ParamKey {
        /**
         * 宽
         * */
        public final static String KEY_VIDEO_WIDTH = "video-width";
        /**
         * 高
         * */
        public final static String KEY_VIDEO_HEIGHT = "video-height";
        /**
         * capture 图像的分辨率
         * */
        public final static String KEY_VIDEO_PREVIEW_SIZE = "video-preview-size";
        /**
         * 支持的分辨率
         * */
        public final static String KEY_VIDEO_SUPPORTED_PREVIEW_SIZES = "video-support-preview-sizes";
        /**
         * 视频帧率
         * */
        public final static String KEY_VIDEO_FRAME_RATE = "video-frame-rate";
        /**
         * 视频码率
         * */
        public final static String KEY_VIDEO_BIT_RATE = "video-bit-rate";
        /**
         * 视频支持的码率
         * */
        public final static String KEY_VIDEO_SUPPORTED_BIT_RATE = "video-supported-bit-rate";
        /**
         * I 帧间隔
         * */
        public final static String KEY_VIDEO_I_FRAME_INTERVAL = "video-i-frame-interval";
        /**
         * 音频通道数
         * */
        public final static String KEY_AUDIO_CHANNEL_NUM = "audio-channel-num";
        /**
         * 音频采样率
         * */
        public final static String KEY_AUDIO_SAMPLE_RATE = "audio-sample-rate";
        /**
         * 音频采样位数
         * */
        public final static String KEY_AUDIO_SAMPLE_BIT = "audio-sample-bit";
        /**
         * 音频采样帧率
         * */
        public final static String KEY_AUDIO_FRAME_RATE = "audio-frame-rate";
    }
}
```



```java
private void LoadParamConfig() {
        IParamConfigManager configManager = IPCServiceManager.getInstance().getService(IPCServiceManager.IPCService.MEDIA_PARAM_SERVICE);

        configManager.setInt(Common.ChannelIndex.E_CHANNEL_VIDEO_MAIN, Common.ParamKey.KEY_VIDEO_WIDTH, 1280);
        configManager.setInt(Common.ChannelIndex.E_CHANNEL_VIDEO_MAIN, Common.ParamKey.KEY_VIDEO_HEIGHT, 720);
        configManager.setInt(Common.ChannelIndex.E_CHANNEL_VIDEO_MAIN, Common.ParamKey.KEY_VIDEO_FRAME_RATE, 20);
        configManager.setInt(Common.ChannelIndex.E_CHANNEL_VIDEO_MAIN, Common.ParamKey.KEY_VIDEO_I_FRAME_INTERVAL, 1);
        configManager.setInt(Common.ChannelIndex.E_CHANNEL_VIDEO_MAIN, Common.ParamKey.KEY_VIDEO_BIT_RATE, 1000_000);

        configManager.setInt(Common.ChannelIndex.E_CHANNEL_AUDIO, Common.ParamKey.KEY_AUDIO_CHANNEL_NUM, 1);
        configManager.setInt(Common.ChannelIndex.E_CHANNEL_AUDIO, Common.ParamKey.KEY_AUDIO_SAMPLE_RATE, 8000);
        configManager.setInt(Common.ChannelIndex.E_CHANNEL_AUDIO, Common.ParamKey.KEY_AUDIO_SAMPLE_BIT, 16);
        configManager.setInt(Common.ChannelIndex.E_CHANNEL_AUDIO, Common.ParamKey.KEY_AUDIO_FRAME_RATE, 25);
    }
```

### **3.获取配网服务开始配网**

```java
INetConfigManager iNetConfigManager = IPCServiceManager.getInstance().getService(IPCServiceManager.IPCService.NET_CONFIG_SERVICE);
iNetConfigManager.configNetInfo(new INetConfigManager.NetConfigCallback() {
            @Override
            public void configOver(String token) {
               //配网完成，开始准备开启推流服务
            }

            @Override
            public void startConfig() {
                android.util.Log.d(TAG, "startConfig: ");
            }

            @Override
            public void recConfigInfo() {//收到配网信息了
                android.util.Log.d(TAG, "recConfigInfo: ");
            }
            
            /**
             * 配网失败，建议提示用户重新操作，不能重试
             * @param type 配网类型 ConfigProvider.TYPE_XX
             * @param msg 错误信息
             */
            @Override
            public void onNetConnectFailed(int type, String msg) {
                Log.w(TAG, "onNetConnectFailed: " + type + " / " + msg);
            }

            /**
             * 配网准备阶段失败，建议重试
             * @param type 配网类型 ConfigProvider.TYPE_XX
             * @param msg 错误信息
             */
            @Override
            public void onNetPrepareFailed(int type, String msg) {
                Log.w(TAG, "onNetPrepareFailed: " + type + " / " + msg);
                iNetConfigManager.retry(type);
            }
            
        });
    }
```

### **4.激活设备**
```java
//获取服务
IMediaTransManager transManager = IPCServiceManager.getInstance().getService(IPCServiceManager.IPCService.MEDIA_TRANS_SERVICE);

/**
 * 激活SDK
 * @param token 配网获得的token
 * @param basePath 可写的一个路径，用于存储SDK相关的配置
 * @param recordPath 可写的一个路径，用于存储录像
 * @param productId 产品Id
 * @param uuid  每个设备的SN
 * @param authorKey 授权的码
 * @return
 */
transManager.initTransSDK(token, basePath, recordPath,
                        productId, uuid, authorKey);

```

### <div id="开始推流">**5.开始推流**</div>

推流需要在设备激活成功后发起，即MQTT上线时

```java

IMqttProcessManager mqttProcessManager = IPCServiceManager.getInstance().getService(IPCServiceManager.IPCService.MQTT_SERVICE);

mqttProcessManager.setMqttStatusChangedCallback(status -> {
                    Log.w("onMqttStatus", status + "");

                    if (status == Common.MqttConnectStatus.STATUS_CLOUD_CONN) {
                    //开启传输
						transManager.startMultiMediaTrans();
						
						}
					}
```
开启传输后就可以向云端推流，视频和音频数据都使用`pushMediaStream`方法

```java
/**
     * push 一帧多媒体流到SDK
     * @param streamType 媒体数据类型 {@link Common.ChannelIndex}
     * @param nalType 是视频流时，为H264码流的NAL类型（Common.NAL_TYPE.NAL_TYPE_IDR 或 Common.NAL_TYPE.NAL_TYPE_PB） 
     * 是音频流时，此参数无效，传0即可
     * @param streamData 码流数据
     * @param timeStamp 每一帧数据产生的时间戳
     * */
    int pushMediaStream(int streamType, int nalType, byte[] streamData, long timeStamp);
```

> #### 注意： <a id="toc_8"></a>
> 
> 如果操作的SDK相关的类的时候是在非主进程中的话，那么获取权限的部分可能会存在一定的问题，这个时候需要在AndnroidManifest.xml中添加如下申明**：**
> 
> \*\*\*\*
> 
> ```markup
> <!-- 如果是跨进程的，那么申明一下所在的进程-->
>         <receiver android:name="com.tuya.smart.aiipc.base.permission.IPCBroadcastReceiver"
>             android:process=":x">
>             <intent-filter>
>                 <action android:name="com.tuya.smart.aiipc.base.permission.BROADCAST_ACTION"/>
>             </intent-filter>
>         </receiver>
> ```
> 
> 将android:process处的值改为和所在进程一样的值。ex:在如下的进程操作的SDK
> 
> 
> 
> ```markup
> <service
>     android:name="com.tuya.smart_doorbell.service.DoorBellService"
>     android:process=":x"  //上面的广播需要和次值保持一致
>     android:enabled="true"
>     android:exported="true">
> </service>
> ```
> 
> 在推送流的时候，关键帧之前必须要加上SPS和PPS的数据
> 
> 
> 
> ```java
> if (info.flags == BUFFER_FLAG_KEY_FRAME) {
>     outputStream.reset();
>     try {
>         outputStream.write(SPS);
>         outputStream.write(PPS);
>         outputStream.write(bytes);
>     } catch (IOException e) {
>         e.printStackTrace();
>     }
>     bytes = outputStream.toByteArray();
>     type = Common.NAL_TYPE.NAL_TYPE_IDR;
> }
> ```



