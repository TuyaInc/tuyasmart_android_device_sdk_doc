---
description: 通过服务端下发的MQTT消息添加设备。
---

# 通过MQTT消息配网
> **使用说明**  
> 接入SDK到设备端并运行，使用*涂鸦智能APP*扫二维码完成配网
> > 二维码生成规则：  
> > https://smartapp.tuya.com/s/p?p=[你的pid]&uuid=[你的uuid]&v=2.0
> > 将上面链接中的参数替换（p对应pid、uuid对应uuid），将链接生成一个二维码
> > 
> > 权限要求：
> > 配网使用的uuid、pid 需要先进行平台录入方可使用，请联系相关对接人（详细录入方式@沫候）

### **1. 配置依赖**

```groovy
    implementation 'com.tonyodev.fetch2:fetch2:3.0.3'
    implementation 'com.tonyodev.fetch2okhttp:fetch2okhttp:3.0.3'
    implementation 'io.reactivex.rxjava2:rxjava:2.2.8'
    implementation 'io.reactivex.rxjava2:rxandroid:2.1.1'
    implementation 'com.squareup.okhttp3:okhttp-urlconnection:3.12.3'
    implementation 'com.google.protobuf:protobuf-javalite:3.8.0'
    implementation 'org.eclipse.paho:org.eclipse.paho.client.mqttv3:1.2.0'
```

### **2. 获取 INetConfigManager**

```java
IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.NET_CONFIG_SERVICE);
```

### **3. 配置authorkey & uuid**

```java
INetConfigManager.setAuthorKey(String authorKey);

INetConfigManager.setUserId(String userId);
```

### **4. 设置配网回调初始化SDK**

```java
iNetConfigManager.configNetInfo(new INetConfigManager.NetConfigCallback() {
            @Override
            public void configOver(boolean first, String token) {
            IMediaTransManager transManager = IPCServiceManager.getInstance().getService(IPCServiceManager.IPCService.MEDIA_TRANS_SERVICE);
            
           	/**			    
            * 初始化流传输SDK
            * @param token 配网获得的token
		     * @param basePath 可写的一个路径，用于存储SDK相关的配置
		     * @param recordPath 可写的一个路径，用于存储录像
		     * @param productId 产品Id
		     * @param uuid  每个设备的SN
		     * @param authorKey 授权的码
		     */
		     
            transManager.initTransSDK(token, basePath, recordPath, productId, uuid, authorKey);
            
            }
        });
```

### 5. 如何关闭该配网模式
```java
ConfigProvider.enableMQTT(false);
```