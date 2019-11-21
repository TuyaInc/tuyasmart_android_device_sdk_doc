---
description: 通过服务端下发的MQTT消息添加设备。
---

# 通过MQTT消息配网
> **使用说明**  
> 接入SDK到设备端并运行，使用*涂鸦智能APP*扫二维码完成配网
> > 二维码生成规则：  
> > https://smartapp.tuya.com/s/p?p=&uuid=&v=2.0
> > 将上面链接中的参数替换（p对应pid、uuid对应uuid），将链接生成一个二维码

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

#### **仅配网接入：**

```java
iNetConfigManager.configNetInfo(new INetConfigManager.NetConfigCallback() {
            @Override
            public void configOver(boolean first, String token) {
            IMediaTransManager transManager = IPCServiceManager.getInstance().getService(IPCServiceManager.IPCService.MEDIA_TRANS_SERVICE);
            
            transManager.initIoTSDK(token, productId, uuid, authorKey);

            }
        });
```

#### 接入IPC：

```java
iNetConfigManager.configNetInfo(new INetConfigManager.NetConfigCallback() {
            @Override
            public void configOver(boolean first, String token) {
            IMediaTransManager transManager = IPCServiceManager.getInstance().getService(IPCServiceManager.IPCService.MEDIA_TRANS_SERVICE);
            
            transManager.initTransSDK(token, "/sdcard/", "/sdcard/", "", "", "");

            }
        });
```

