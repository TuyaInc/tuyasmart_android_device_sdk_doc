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
            
     
     			/**
			     * 初始化流传输SDK, 关闭了p2p验证
			     * @param token 配网获得的token
			     * @param productId 产品Id
			     * @param uuid  每个设备的SN
			     * @param authorKey 授权的码
			     */
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

### 4. 如何关闭该配网模式
```java
ConfigProvider.enableBluetooth(false);
```
