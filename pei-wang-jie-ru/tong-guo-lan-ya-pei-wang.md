---
description: 通过涂鸦智能APP“自动发现”添加设备。
---

# 通过蓝牙配网

### 1**. 获取 INetConfigManager**

```java
IPCServiceManager.getInstance()
.getService(IPCServiceManager.IPCService.NET_CONFIG_SERVICE);
```

### **2. 设置PID**

```java
INetConfigManager.setPid(String pid);
```

### **3. 设置配网回调初始化SDK**

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

