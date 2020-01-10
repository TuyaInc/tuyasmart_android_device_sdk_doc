---
description: 通过扫描涂鸦智能APP生成的二维码添加设备。
---

# 通过WiFi配网

### 1**. 获取 INetConfigManager**

```java
IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.NET_CONFIG_SERVICE);

//在界面中提供扫码预览SurfaceView
SurfaceView surfaceView = findViewById(R.id.surface);

iNetConfigManager.config(INetConfigManager.QR_OUTPUT, surfaceView.getHolder());
```

### **2. 设置配网回调初始化SDK**

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

**接入IPC:**

```java
iNetConfigManager.configNetInfo(new INetConfigManager.NetConfigCallback() {
            @Override
            public void configOver(boolean first, String token) {
            IMediaTransManager transManager = IPCServiceManager.getInstance().getService(IPCServiceManager.IPCService.MEDIA_TRANS_SERVICE);
            
            transManager.initTransSDK(token, "/sdcard/", "/sdcard/", "", "", "");

            }
        });
```
### 3. 如何关闭该配网模式
```java
ConfigProvider.enableQR(false);
```
